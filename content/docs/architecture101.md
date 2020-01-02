---
title: "Architecture 101"
# bookFlatSection: false
# bookToc: 6
# bookHidden: false
---
# Architecture 101
## Access Management Basics
* *Principal* a person or service that can make _authenticated_ or _anonymous_ request to perform an action on a system
* *Authentication* process of identification (with username/password, keys)
* *Identity* Objects which require _authentication_  and are _authorized_ to access resource
* *Authorization* Process of checking and allowing (or denying acces for identity)

# Shared responsibility model

{{< columns >}}
## Customer
Customer is responsible for security **in** the cloud
* Customer data
* Platform, application, access management, encryption (at rest/in transit)
* OS, network, firewall configuration
<--->
## AWS
AWS is responsible for security **off** the cloud
* **Software** DB, Network, compute, storage
* **Hardware** Regions, AZs, Edge locations
{{< /columns>}}

## Service Models

* *IaaS* - Infrastructue as a service
* *PaaS* - Platform as a service
* *SaaS* - Software as a service

IaaS               |PaaS               |SaaS               |
-------------------|-------------------|-------------------|
**Data**           |**Data**           |**Data**           |
**Application**    |**Application**    |Application        |
**Runtime**        |Runtime            |Runtime            |
**OS**             |OS                 |OS                 |
Virtualization     |Virtualization     |Virtualization     |
Hosts/Servers      |Hosts/Servers      |Hosts/Servers      |
Networkind/Storage |Networkind/Storage |Networkind/Storage |
Data Center        |Data Center        |Data Center        |

## Hig Availability vs Fault Tolerance
* **HA** is ability to recover quickly in case of failure
    * Example _Car_ (in case if wheel blows up it's fine to stop and change wheel)
{{< mermaid >}}
    graph LR
        Failure --> Terminate
        Terminate --> Recover
{{< /mermaid >}}
* **FT** System designed to operate through the failure
    * Example _Plane_ (in case of **one** engine failure, plane usually continues flight)
    {{< mermaid >}}
    graph LR
        LB[Load Balancer]
        LB -->  A["Instance (failed)"]
        LB -->  B[Instance]
        LB -->  C[Instance]
        style A fill:#f9f
    {{< /mermaid >}}

## Disaster recovery 
* **Recovery Point Objective (RPO)** How much can company loose (in time). The maximum time between a table and backup
* **Tecovery Time Objective (RTO)** The maximum amount of time you can recover.

## Scaling Architecture
* **Vertical** Additional resources (CPU, Memory, etc)
* **Horizontal** Add additional smaller instances. Requires application support

## Tiered Architecture 
* Presentation
* Logic 
* Data

## Encryption 
Can be either **In Transit** or **At rest**
Can be **Symmetric** and **Assimetric**

## Architecture Odds and Ends
* **Cost effective**
* **Secure**
* **Application session state**
* **Undifferiented heavy lifting**
