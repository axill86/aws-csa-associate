---
title: "Multi-Account Management and Organizations"
weight: 1
# bookFlatSection: false
# bookToc: 6
# bookHidden: false
---
# Multi-Account Management and Organizations

## AWS Organizations
**AWS Organizations** is a service for managing multiple consolidated accounts, which belongs to the same organization. It also allows to perform consolidated billing, when bills from all organizaiton collected into single account. 
Organization accounts can be grouped into **organizational units**. 

{{< mermaid >}}
    graph TD;
        root[Root Account]
        ou[Organizational Unit]
        ou1[Organizational Unit]
        ou3[Organizational Unit]
        acc[Account]
        acc1[Account]
        acc2[Account]
        acc3[Account]
        root --> ou
        ou --> acc
        ou --> acc1
        
        root --> ou1
        ou1 --> acc2
        ou1 --> acc3
        ou1 --> ou3
{{< /mermaid >}}
**Service Control Policies** are used for limiting account usage. Those can be appliced to **OU** or **Accounts**
* [AWS Documentation](https://docs.aws.amazon.com/controltower/latest/userguide/organizations.html)

## Role Switching

**Role Switching** is a methond of accessing one account from another using set of credentials.

1. A role in **Account B** trutsts **Account A**
1. An identity in **Account A** can _assume_ role in **Account B**
1. An identity from **Account A** can operate in **Account B** with this role