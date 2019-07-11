# cisco-nso-first-dive

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




# References


* https://www.youtube.com/watch?v=AGVChkovQ7s
*
