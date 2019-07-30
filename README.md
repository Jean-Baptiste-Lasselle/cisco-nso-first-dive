# Nombre de minutes en une semaine

![Nb min en une semaine](https://github.com/Jean-Baptiste-Lasselle/cisco-nso-first-dive/raw/master/documentation/images/NOMBRE_MINUTES_EN_UNE_SEMAINE_2019-07-29%2023-37-21.png)

Références à ajouter pour le passage sur une branche `export LA_BRANCHE_MANAGERIALE` : 

* https://confluence.atlassian.com/bitbucket/checkout-a-branch-into-a-local-repository-313466957.html
* https://stackoverflow.com/questions/4470523/create-a-branch-in-git-from-another-branch

On exécute la commande `git checkout $LA_BRANCHE_MANAGERIALE`, ainsi en créant une nouvelle branche à partir de cet état, on créée la branche en partant du dernier commit de la branche `$LA_BRANCHE_MANAGERIALE`.

On aura ausi une recette de la forme : 

```bash
export GITLAB_HOSTNAME=gitlab.com
export ACCESS_TOKEN_DU_USER=NaSCLm68YWq2dH38A_eJ

# sudo yum install -y jq yq

# ----------------------------------------------------------------------------------------------------------------------
# ----------------------------------------------------------------------------------------------------------------------
# ----------------------------------------------------------------------------------------------------------------------
# 
# Exemple typique : 
# 
# => Utilisation d'une branche de travail créée à partir d'un branche de validation managériale
#    et envoi automatique de la merge request
#  
# ----------------------------------------------------------------------------------------------------------------------
# ----------------------------------------------------------------------------------------------------------------------
# ----------------------------------------------------------------------------------------------------------------------


export NOM_DE_MA_BRANCHE_DE_TRAVAIL=feature-xxx

# Creates MyFeature branch off of the last commit on the '$LA_BRANCHE_MANAGERIALE' branch. 
git checkout -b $NOM_DE_MA_BRANCHE_DE_TRAVAIL $LA_BRANCHE_MANAGERIALE

# Then you just code (edit files), aka do your work, and then

# 
# 'git commit -a' automatically stage all tracked, modified files before the commit 
# If you think the git add stage of the workflow is too cumbersome, Git allows you to
# skip that part with the -a option. This basically tells Git to run git add on any file that 
# is "tracked" - that is, any file that was in your last commit and has been modified.
# 

export COMMIT_MESSAGE=""
COMMIT_MESSAGE="$COMMIT_MESSAGE Your commit message. Respect."


# Now we will just push the new commits, and won't merge localy, but in th staed wil use Gitlab's RESTful API to send a merge request

git add --all && git commit -m "COMMIT_MESSAGE" && git push

# So no local merge of your changes to dev (with or without a fast-forward)


# Finally , calling the Gitlab's RESTful API to create a new merge request (which will require a manager's gonogo) :  

echo "https://github.com/gitlabhq/gitlabhq/blob/master/doc/api/merge_requests.md#create-mr"



export NOM_DU_REPO_DE_LA_MERGE_REQUEST=mock-repo-tgs



export ID_DU_REPO_SUR_LEQUEL_FAIRE_LA_MERGE_REQUEST=$(curl --header "PRIVATE-TOKEN: $ACCESS_TOKEN_DU_USER" -X GET "https://$GITLAB_HOSTNAME/api/v4/projects?$GET_REQ_PARAMS" | jq --arg REPO_NAME "$NOM_DU_REPO_DE_LA_MERGE_REQUEST"  '.[] | select(.name==$REPO_NAME)' | jq .id)


export MERGE_REQUEST_CREATION_PAYLOAD="{ \"source_branch\": \"$NOM_DE_MA_BRANCHE_DE_TRAVAIL\", \"target_branch\": \"$LA_BRANCHE_MANAGERIALE\" }"

# 
# Endpoint POST /projects/:id/merge_requests
# 
curl -H "Content-Type: application/json" -H "PRIVATE-TOKEN: $ACCESS_TOKEN_DU_USER" -X POST --data "$MERGE_REQUEST_CREATION_PAYLOAD" https://$GITLAB_HOSTNAME/api/v4/projects/$ID_DU_REPO_SUR_LEQUEL_FAIRE_LA_MERGE_REQUEST/merge_requests




# ----------------------------------------------------------------------------------------------------------------------
# ----------------------------------------------------------------------------------------------------------------------
# ----------------------------------------------------------------------------------------------------------------------
# 
# Exemple du cas d'une application NodeJS : 
# 
# => Création automatique et 'silencieuse' du repo git mock du repo git
#    permettant les tests / démos / pocs de workflow git
#  
# ----------------------------------------------------------------------------------------------------------------------
# ----------------------------------------------------------------------------------------------------------------------
# ----------------------------------------------------------------------------------------------------------------------

export ACCESS_TOKEN_DU_USER=NaSCKh68YWq2dH38A_eJ
# export ACCESS_TOKEN_DU_USER=RURab-tb5wdsTH72L55v
export NEW_REPO_NAME=mon-appli-nodejs
export GITLAB_GROUP_INTO_WHICH_TO_CREATE_REPO=playground
export GITLAB_HOSTNAME=gitlab.com

# La seule manière d'obtenir tous mes groupes est de n'utiliser
# qu'un et un seul paramètre à la requête HTTP/GET, 'per_page', et son 
# paramètre associé qui permet de préciser le numéro de page
export I_KNOW_I_HAVE_LESS_GROUPS_THAN_THAT=1000
export GET_REQ_PARAMS="per_page=$I_KNOW_I_HAVE_LESS_GROUPS_THAN_THAT"



# Affiche directement le groupe gitlab '$GITLAB_GROUP_INTO_WHICH_TO_CREATE_REPO', contenu dans le groupe 'mon.bureau'

curl --header "PRIVATE-TOKEN: $ACCESS_TOKEN_DU_USER" -X GET "https://$GITLAB_HOSTNAME/api/v4/groups?$GET_REQ_PARAMS" | jq --arg GRP_NAME "$GITLAB_GROUP_INTO_WHICH_TO_CREATE_REPO"  '.[] | select(.name==$GRP_NAME)'

# 
# 
# => Je veux que le repo ait  pour URL finale :
#             https://gitlab.com/mon.bureau/$GITLAB_GROUP_INTO_WHICH_TO_CREATE_REPO/$NEW_REPO_NAME
# 
# C'est à dire que le nouveau repository git soit placé dans le groupe de repos  'mon.bureau/$GITLAB_GROUP_INTO_WHICH_TO_CREATE_REPO'
# 
# Stocke l'ID recherché, du groupe [$GITLAB_GROUP_INTO_WHICH_TO_CREATE_REPO], dans la variable [$ID_DU_GROUPE_CIBLE]
export ID_DU_GROUPE_CIBLE=$(curl --header "PRIVATE-TOKEN: $ACCESS_TOKEN_DU_USER" -X GET "https://$GITLAB_HOSTNAME/api/v4/groups?$GET_REQ_PARAMS" | jq --arg GRP_NAME "$GITLAB_GROUP_INTO_WHICH_TO_CREATE_REPO"  '.[] | select(.name==$GRP_NAME)' | jq .id)

echo "ID_DU_GROUPE_CIBLE=$ID_DU_GROUPE_CIBLE "


export REPO_CREATION_PAYLOAD="{ \"name\": \"$NEW_REPO_NAME\", \"namespace_id\": \"$ID_DU_GROUPE_CIBLE\" }"

echo "REPO_CREATION_PAYLOAD : "
echo "{$REPO_CREATION_PAYLOAD}"
curl -H "Content-Type: application/json" -H "PRIVATE-TOKEN: $ACCESS_TOKEN_DU_USER" -X POST --data "$REPO_CREATION_PAYLOAD" https://$GITLAB_HOSTNAME/api/v4/projects

echo "Ce script devra être testé pour le cas où deux groueps de même noms soient créés comme sous-groupes de deux groupes distincts."
echo "Ce script devra évoluer pour permettre à son utilisateur de préciser lui-même directement l' [ID_DU_GROUPE_CIBLE=$GITLAB_HOSTNAME] "

# 
# TODO : List project's merge requests
# 
# GET /projects/:id/merge_requests
# GET /projects/:id/merge_requests?state=opened
# GET /projects/:id/merge_requests?state=all
# GET /projects/:id/merge_requests?iids[]=42&iids[]=43
# GET /projects/:id/merge_requests?milestone=release
# GET /projects/:id/merge_requests?labels=bug,reproduced
# GET /projects/:id/merge_requests?my_reaction_emoji=star
# 

if [ -f ./API_CALL_GET_PARAMS.list ]; then
  rm -f ./API_CALL_GET_PARAMS.list
fi

echo "state=all" >> ./API_CALL_GET_PARAMS.list
echo "state=opened" >> ./API_CALL_GET_PARAMS.list
echo "iids[]=37&iids[]=43" >> ./API_CALL_GET_PARAMS.list
echo "milestone=canary-wave2" >> ./API_CALL_GET_PARAMS.list
echo "labels=devops,bug,reproduced" >> ./API_CALL_GET_PARAMS.list
echo "my_reaction_emoji=star" >> ./API_CALL_GET_PARAMS.list
echo "my_reaction_emoji=dadjoke" >> ./API_CALL_GET_PARAMS.list


while read CURRENT_LIST_MERGE_REQUEST_GET_REQ_PARAMS; do
  echo "CURRENT_LIST_MERGE_REQUEST_GET_REQ_PARAMS=[$CURRENT_LIST_MERGE_REQUEST_GET_REQ_PARAMS]"
  export LIST_MERGE_REQUEST_GET_REQ_PARAMS=$CURRENT_LIST_MERGE_REQUEST_GET_REQ_PARAMS
  # So finally calling Gitlab's RESTful API v4 through its neat GraphQL new skin 
  curl --header "PRIVATE-TOKEN: $ACCESS_TOKEN_DU_USER" -X GET "https://$GITLAB_HOSTNAME/api/v4/projects/$ID_DU_REPO_SUR_LEQUEL_FAIRE_LA_MERGE_REQUEST/merge_requests?$LIST_MERGE_REQUEST_GET_REQ_PARAMS" | jq '.[]'
done <./API_CALL_GET_PARAMS.list

```

* https://gitlab.com/second-bureau/pegasus/pipeline-step-lab/tree/master/docker/git  (recette prête de l'invocation de l'API dans tous les ues cases des workflows)


# Cisco-nso-first-dive

A first dive ito Cisco 's NSO Network Service Orchestrator, to see what's there related to SDN. And how to setup a proper Infrastructure As Code toolchain  

## Summing up

* The `ncs-project` tool : 
  * what is it? Is it like the old `ant`?
  * https://community.cisco.com/t5/nso-developer-hub-blogs/auto-generate-nso-templates-based-on-cli-configuration/ba-p/3663264
  * https://community.cisco.com/t5/nso-developer-hub-documents/nso-projects/ta-p/3635219
  * so litteraly : 
  > The `ncs-project` tool is bundled with NSO and can be used to create a new project


## Analyzing the Cisco NSO Devops whitepaper

https://github.com/Jean-Baptiste-Lasselle/cisco-nso-first-dive/blob/master/documentation/externe/cisco/nso-bridge-automation.pdf  




### Phase 1: Build a programmable network interface

`NSO` provides a better way using the configuration 
datastore (`CDB`) and the abstraction/normalization of 
the network element drivers (`NEDs`) to provide a much 
more robust and resilient way of handling configuration 
management through two mechanisms:

_**Transactions**_

Configuration changes are handled like database 
transactions: all changes are applied at once, and if any 
part of the change fails, the entire transaction rolls back.

_**Synchronization mechanism and diff engine**_

`NSO` can compare the configuration in the `CDB` to 
a device and highlight differences. `NSO` can also 
synchronize in either direction. It can bring the device 
back in line with what the `CDB` expects or update with 
`CDB` with the device configuration (i.e., to capture out-
of-band updates).
These two mechanisms combine to ensure configuration 
changes are implemented in a trusted fashion:

*  `NSO` receives intent (what the network should look like).
*  `NSO` compares the desired state to the current state and 
presents a “`diff`” before proceeding. 
* `NSO` updates the device to match the desired state.
* `NSO` then reads back the device configuration to ensure 
it matches the desired state.

`NSO` manages device configurations for the entire 
network with a single interface and consistent syntax. 
Network engineers and operations teams can use 
the same tools they use now—CLI scripting or `REST` 
interfaces—to manipulate the configuration lifecycle 
of devices as a single set.

The devices can be grouped, an their configurations can be based on templates called `golden configuration`.
`golden configurations` can be updated, continuously.

Once `golden configurations` are applied, network 
engineers and operations teams can use `NSO` to poll 
the network for any element that deviates from the 
template, and either make the device comply with the _golden configuration_, or allowing the device to break the _golden rule_, but explicitly, and under permission control, certainly. 

Bout _the gold rule_ : Oh yes, I'm pretty sure `Cisco` named those templates _golden configurations_, thinking of them as _golden rules_ (those rules you should never ever break), engraved in the _golden configurations_. _Golden rules_ applied to the network as a whole, indeed.

 `Network Elements Drivers (NEDs)` are the components of `NSO` that makes it capable of supporting Multi Vendor Devices. Cf.  : 
 
* https://www.cisco.com/c/en/us/products/collateral/cloud-systems-management/network-services-orchestrator/datasheet-c78-734669.html
* https://github.com/Jean-Baptiste-Lasselle/cisco-nso-first-dive/blob/master/documentation/externe/cisco/NEDs/README.md


### Phase 2: Service abstraction

This part essentially is the _infrastructure as a service_ service : what the users of `NSO` will use to provision and operate their networks.

**_`dry-run` capabilities_**

The `NSO` network change tool shows how a planned 
change will affect the network and services before 
executing it. Before **committing** to a change, teams can 
perform a dry run and see the minimum set of changes 
that will occur in the network as the change is executed. 

_**Activation testing**_

You have the tools to build canary tests for new and 
changed services by sending active traffic over the new 
(or newly changed) service, measure customer-facing 
key performance indicators (KPIs), and verify that the 
service is performing as expected


**_analysis tools_**

Various tools are there bundled with `NSO` to diagnostic network issues.


### Phase 3: Full DevOps infrastructure automation

#### Yang Models

TO make Infrastructure as code possible, NSO is Model based, and more specifically based on `YANG` models concepts : 
It's just like `UML` but to specify a network, insted of a software.


#### FastMap / Reactive FastMap

Those two are designed so that `NSO` works to continually converge the network 
towards the _**desired state**_

_FastMap_

Developers only need describe the “create” operations 
for a service. FastMap automatically determines the 
update, delete, and repair operations needed for 
any type of run-time service modification, saving the 
developer the time and effort to define workflows for 
every conceivable service lifecycle scenario.

_Reactive FastMap_

Ideal for multi-domain and  distributed environments : 
Reactive FastMap takes a non-linear approach to 
implementing necessary changes needed to reach a 
desired state. Some changes (i.e., apply a new firewall 
rule) might take seconds to implement while others 
(i.e., spin up a new VM) might take minutes. Instead of 
getting stuck waiting on changes to complete, Reactive 
FastMap makes changes where it can and continually re-
evaluates what still needs to be done

Meaning the FastMap work is parallelized

_Package management_

`NSO` gives developers a comprehensive, systematic 
approach to package management with tools to 
manage applications on top of the platform through 
the full lifecycle of installing, updating, and uninstalling 
packages. The platform applies strict versioning rules 
and allows developers to capture dependencies 
between packages. 


#### Northbound integration `APIs` 

To support DevOps processes and serve and an 
effective bridge, `NSO` provides a stable, flexible software 
interface:

* A rich **set of northbound APIs** : `NSO` supports APIs ranging from programmatic or RPC-based protocols (such as `NETCONF`/`RESTCONF`) to language bindings like Erlang, Java, Python, and C. `NSO` also provides human-to-machine interfaces, such as a web UI and a set of CLIs. All of these interfaces are automatically rendered from the models that developers create. 
* **API mediation** : A common impediment service provider developers face is existing OSS/BSS systems with hard-coded southbound calls to infrastructure. With conventional orchestration systems, service providers have to undertake an extensive integration project to change how OSS systems parse parameters to the orchestrator. `NSO` simply adapts to the existing APIs the `OSS` uses. Developers can create data models with that `API`, load them into `NSO`, and map it to the existing service package. The example is `SP-specific`, but `NSO` can provide similar `API` mediation for enterprise systems.

* **Verify** : `NSO` provides development and production test capabilities through its `NetSim` tool (it's a network simulator). This network simulator allows developers to quickly and inexpensively test their code on a realistic simulation of the production environment. `NSO` also provides offline tools for **validating version migration**. These tools validate the extent to which clients or consumers of a service (i.e., an orchestrator or a OSS/BSS system) need updates, so 
developers can avoid introducing unintended disruptive changes.

* **Package** : When developers release new code, `NSO` provides a self-contained and versioned package format. This 
means that developers can build and package their work such that the package is the only thing they need to import into the running system. `NSO` also provides hitless package installation and version migration, so developers can introduce new packages or update existing ones at run time, without impacting the operation of the system.
* **Configure** : `NSO` can integrate into a `CI/CD` pipeline so that infrastructure and infrastructure configuration can be seamlessly deployed in concert with the related software packages. Beyond simplifying initial deployment, this capability is helpful with functions like auto-scaling so adding or deleting app instances also automatically includes the associated infrastructure.
* **Monitor** : 
`NSO` provides insight to understand how an app or service is interacting with the infrastructure--is there a 
performance bottleneck or is a service running out of resources. The `CDB` also provides a single source of 
truth for performance management, health monitoring, system assurance and similar tools to easily gather operational data on the state of infrastructure.  

> 
> ### Lexique
> 
> `OSS` : Un `Operations Support System` ou un `Operational Support System` est l'ensemble des composants opérationnels ou les systèmes informatiques utilisés par un _opérateur de télécommunications_. Elle est synonyme de maintenance opérationnelle dans le domaine des télécommunications.
> 

# ANNEX : ALTERNATIVE NETWORK SIMULATORS

* https://shadow.github.io/ 
* https://github.com/akeranen/the-one  (nokia )
* https://github.com/imunes/imunes (docker openVswithc, etc..)
* https://github.com/CovenantSQL/GNTE  (uses `docker` too)
* https://github.com/stripe-ctf/octopus
* https://github.com/mininet/mininet
* https://github.com/umardx/automarked 


# ANNEX : NETWORK automation

* saltstack / napalm : 
  * https://github.com/napalm-automation/napalm-logs  (nomalization of network devices logging stream)
  * https://github.com/saltstack-formulas/napalm-ntp-formula 
  * https://github.com/saltstack-formulas/napalm-bgp-formula 
  * https://github.com/saltstack-formulas/napalm-interfaces-formula 
  * https://github.com/saltstack-formulas/napalm-lldp-formula 
  * https://github.com/saltstack-formulas/napalm-users-formula 
* ansible / napalm : 
  * https://github.com/napalm-automation/napalm-ansible
* napalm : https://github.com/napalm-automation/napalm

# Ansible et Cisco NSO 

Il existe 3 modules ansible pour NSO, et voici un white paper ansible / nso : https://github.com/Jean-Baptiste-Lasselle/cisco-nso-first-dive/blob/master/documentation/externe/cisco/1012-oaa-ckn.pdf

* The `nso_verify` module fetches data from `NSO`, compares with 
* The `nso_action`module performs RPCs on `NSO` (e.g. check-sync) and validates the output
* The `nso_config` module is used to create and delete instance data in `NSO`


# References


* https://www.youtube.com/watch?v=AGVChkovQ7s

* https://dtucker.co.uk/work/netconf-yang-restconf-and-netops-in-an-sdn-world.html :  dans cet article, l'auteur évoque l'intérêt de la _Northbound API_ pour l'accès au niveau _devices_.
* https://dzone.com/articles/5-steps-to-automated-netops
* https://github.com/cilium/cilium/
* https://github.com/logzilla/logzilla-opengear

# Just funny

* https://github.com/sartura/network-plugin-openwrt


