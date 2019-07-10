# Tout la documentation officielle Cisco que j'ai pu récupérer, sur l'outil `ncs-project` :

* qui permet entre autre de créer un nouveau projet `NSO`, 
* qui permet de faire le build  d'un projet `NSO` avec l'outil `make`
* pour le déploiement, l'étude est à approfondir; 



# Doc offiicielle `ncs-project`

Source : https://community.cisco.com/t5/nso-developer-hub-documents/nso-projects/ta-p/3635219



### The ncs-project tool

The ncs-project tool is bundled with NSO and can be used to create a new project:

```bash
# ncs-project create my-project

Creating directory: /Users/frjansso/tmp/my-project

Using NCS 4.4.2.2 found in /Users/frjansso/dev/nso-4.4.2.2

wrote project to /Users/frjansso/tmp/my-project

that generates a directory structure where NSO can be run:

# find my-project

my-project

my-project/init_data

my-project/logs

my-project/Makefile

my-project/ncs-cdb

my-project/ncs.conf

my-project/packages

my-project/project-meta-data.xml

my-project/README.ncs

my-project/setup.mk

my-project/state

...


# cd my-project

# ncs-project update -v -y

ncs-project: installing packages...

ncs-project: installing packages...ok

ncs-project: resolving package dependencies...

ncs-project: resolving package dependencies...ok

ncs-project: determining build order...

ncs-project: determining build order...ok

ncs-project: determining ncs-min-version...

ncs-project: determining ncs-min-version...ok

# make all start

(for i in ; do \

       /Library/Developer/CommandLineTools/usr/bin/make -C packages/${i}/src all || exit 1; \

done)

if [ ! -d ncs-cdb ]; then mkdir ncs-cdb; fi

if [ ! -d init_data ]; then mkdir init_data; fi

cp init_data/* ncs-cdb/. > /dev/null 2>&1 || true

ncs --stop || true

connection refused (stop)

ncs

#
```

So now we have NSO running in this directory, not very interesting since we don't have any packages yet.

### Git

This project should be checked into git

```bash
# git init .

Initialized empty Git repository in /Users/frjansso/tmp/my-project/.git/
```

Now there are a bunch of files we don't want to check in, e.g. the files in logs, ncs-cdb and in state, I typically solve this using .gitignore files.

A simple such file looks like:


```
*
!.gitignore
```

Which tells git to ignore all files but the .gitignore files itself.

So let's create such files in logs, ncs-cdb and in state

# echo "*\n\!.gitignore" | tee logs/.gitignore ncs-cdb/.gitignore state/.gitignore

ncs-project also generates setup.mk files, I don't want to check those in to git either, so I'll create a .gitignore in the top directory to ignore those:

# echo "setup.mk*" >> .gitignore
```

And now we add the other files to git.

```bash
# git add .

# git status

On branch master

No commits yet

Changes to be committed:

  (use "git rm --cached <file>..." to unstage)

  new file:   .gitignore

  new file:   Makefile

  new file:   README.ncs

  new file:   logs/.gitignore

  new file:   ncs-cdb/.gitignore

  new file:   ncs.conf

  new file:   project-meta-data.xml

  new file:   state/.gitignore

  new file:   test/Makefile

  new file:   test/internal/Makefile

  new file:   test/internal/lux/Makefile

  new file:   test/internal/lux/basic/Makefile

  new file:   test/internal/lux/basic/run.lux

  new file:   test/pkgtest.env

#  git commit -am "Initial commit"

Adding local packages

A project isn't very interesting w/o any packages.

To add a local package I'll go to the packages directory and use the ncs-make-package tool

# cd packages

# ncs-make-package --service-skeleton template my-service

# git add my-service

# cd ..
```

To add it to the build system, I'll edit project-meta-data.xml to include my-service as a local package:

```xml
  <package>

    <name>my-service</name>

    <local/>

  </package>
```

I'll run ncs-project again to get the change and then build everything:

```bash
# ncs-project update -y

# make all

(for i in my-service; do \

       /Library/Developer/CommandLineTools/usr/bin/make -C packages/${i}/src all || exit 1; \

done)

mkdir -p ../load-dir

/Users/frjansso/dev/nso-4.4.2.2/bin/ncsc  `ls my-service-ann.yang  > /dev/null 2>&1 && echo "-a my-service-ann.yang"` \

              -c -o ../load-dir/my-service.fxs yang/my-service.yang

if [ ! -d ncs-cdb ]; then mkdir ncs-cdb; fi

if [ ! -d init_data ]; then mkdir init_data; fi

cp init_data/* ncs-cdb/. > /dev/null 2>&1 || true

# ncs_cli -u admin -C

admin connected from 127.0.0.1 using console on FRJANSSO-M-C1DA

admin@ncs# packages reload

>>> System upgrade is starting.

>>> Sessions in configure mode must exit to operational mode.

>>> No configuration changes can be performed until upgrade has completed.

>>> System upgrade has completed successfully.

reload-result {

    package my-service

    result true

}

```

### Adding non local packages

Let's say I want to reuse another package in git, e.g. the IP address allocator:

Again I edit `project-meta-data.xml` :

```xml
  <packages-store>

    <git>

      <repo>ssh://git@stash.tail-f.com/pkg</repo>

    </git>

  </packages-store>

  <package>

    <name>ipaddress-allocator</name>

  </package>
```

```bash
# ncs-project update -v

ncs-project: installing packages...

ncs-project: found local installation of "my-service"

ncs-project: updating package ipaddress-allocator...

ncs-project: Running "cd /Users/frjansso/tmp/my-project/packages/ipaddress-allocator; git rev-parse --show-toplevel".

ncs-project: cd /Users/frjansso/tmp/my-project/packages/ipaddress-allocator

ncs-project: git stash   # (to save any local changes)

ncs-project: git checkout -q "master"

ncs-project: git fetch

ncs-project: git reset --hard origin/master

ncs-project: updating package ipaddress-allocator...done

ncs-project: installing packages...ok

ncs-project: resolving package dependencies...

ncs-project: checking dependencies for "ipaddress-allocator"

ncs-project: found dependency "nso-util"

ncs-project: found dependency "resource-manager"

ncs-project: git clone "ssh://git@stash.tail-f.com/pkg/resource-manager.git" "/Users/frjansso/tmp/my-project/packages/resource-manager"

ncs-project: git checkout -q "master"

ncs-project: git clone "ssh://git@stash.tail-f.com/pkg/nso-util.git" "/Users/frjansso/tmp/my-project/packages/nso-util"

ncs-project: git checkout -q "master"

ncs-project: checking dependencies for "nso-util"

ncs-project: checking dependencies for "resource-manager"

ncs-project: checking dependencies for "my-service"

ncs-project: resolving package dependencies...ok

ncs-project: determining build order...

ncs-project: determining build order...ok

ncs-project: determining ncs-min-version...

ncs-project: determining ncs-min-version...ok

# ls packages

ipaddress-allocator my-service          nso-util            resource-manager
```

As you can see, ncs-project pulls all the dependencies needed as well

```bash
# make all

...

# ncs_cli -u admin -C

...

#

admin@ncs# packages reload

>>> System upgrade is starting.

>>> Sessions in configure mode must exit to operational mode.

>>> No configuration changes can be performed until upgrade has completed.

>>> System upgrade has completed successfully.

reload-result {

    package ipaddress-allocator

    result true

}

reload-result {

    package my-service

    result true

}

reload-result {

    package nso-util

    result true

}

reload-result {

    package resource-manager

    result true

}
```

Keeping Git tidy

When building the packages you will get a bunch of generated files, .class, .jar, .fxs etc. Typically you don't want to check these into git, use .gitignore files to fix this.

If I run git status, I'll see this:


```bash
# git status

...

Untracked files:

  (use "git add <file>..." to include in what will be committed)

  .build-meta

  packages/ipaddress-allocator/

  packages/nso-util/

  packages/resource-manager/

I don't want to version control the external packages here (they have their own repo), so I'll update my .gitignore:

# echo "packages/ipaddress-allocator" >> .gitignore

# echo "packages/nso-util" >> .gitignore

# echo "packages/resource-manager" >> .gitignore
```
