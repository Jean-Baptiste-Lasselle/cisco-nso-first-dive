# cisco-nso-first-dive
A firsst dive ito Cisco 's NSO Network Service Orchestrator, to see what's there related to SDN. And how to setup a proper Infrastructure As Code toolchain  

## Summing up

* The `ncs-project` tool : 
  * what is it? Is it like the old `ant`?
  * https://community.cisco.com/t5/nso-developer-hub-blogs/auto-generate-nso-templates-based-on-cli-configuration/ba-p/3663264
  * https://community.cisco.com/t5/nso-developer-hub-documents/nso-projects/ta-p/3635219
  * so litteraly : 
  > The `ncs-project` tool is bundled with NSO and can be used to create a new project


Let there be https://github.com/Jean-Baptiste-Lasselle/cisco-nso-first-dive/blob/master/documentation/externe/cisco/nso-bridge-automation.pdf : 

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


### Phase 2: Service abstraction

This part essentially is the _infrastructure as a service_ service : what the users of NSO will use to provision and operate their networks.

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


**_For the Devops_**

`Northbound integration APIs` 

To support DevOps processes and serve and an 
effective bridge, `NSO` provides a stable, flexible software 
interface:

* A rich **set of northbound APIs** : `NSO` supports APIs ranging from programmatic or RPC-based protocols (such as `NETCONF`/`RESTCONF`) to language bindings like Erlang, Java, Python, and C. `NSO` also provides human-to-machine interfaces, such as a web UI and a set of CLIs. All of these interfaces are automatically rendered from the models that developers create. 
* **API mediation** : A common impediment service provider developers face is existing OSS/BSS systems with hard-coded southbound calls to infrastructure. With conventional orchestration systems, service providers have to undertake an extensive integration project to change how OSS systems parse parameters to the orchestrator. `NSO` simply adapts to the existing APIs the `OSS` uses. Developers can create data models with that `API`, load them into `NSO`, and map it to the existing service package. The example is `SP-specific`, but `NSO` can provide similar `API` mediation for enterprise systems.

> 
> ### Lexique
> 
> `OSS` : Un `Operations Support System` ou un `Operational Support System` est l'ensemble des composants opérationnels ou les systèmes informatiques utilisés par un _opérateur de télécommunications_. Elle est synonyme de maintenance opérationnelle dans le domaine des télécommunications.
> 




### Phase 3: Full DevOps infrastructure automation

ccc



# References


* https://www.youtube.com/watch?v=AGVChkovQ7s
*
