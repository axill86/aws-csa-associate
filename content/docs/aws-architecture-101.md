---
title: "AWS Architecture 101"
# bookFlatSection: false
# bookToc: 6
# bookHidden: false
---
# AWS Architecture 101
## Accounts
* AWS accounts are independent _by default_
* Consolidated billing for multiple accounts can be set up

## AWS Physical and Networking Layers

**Regions** contain multiple **Availability zones**. Most services operate inside AZ. 
**Edge Location** are small centers which are close to major populations. Used for edge computing and content delivery.
### Links
* [AWS Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)
* [AWS Infrastructure](https://www.infrastructure.aws/)

## AWS Well-Architected Framework

[AWS Well-Architected Framework](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf) describe following key points:
* Security
* Reliablility
* Performance Efficiency
* Operational Excellence
* Cost Optimization

## Elasticity 

Types of Scaling:
* **Vertical** (More CPU/Memory)
* **Horizontal** (More smaller instances)
* **Elastic** Number of instances automated in order to match load and capacity

