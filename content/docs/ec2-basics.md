---
title: "EC2 Basics"
weight: 1
# bookFlatSection: false
# bookToc: 6
# bookHidden: false
---
# EC2 Basics

**EC2** should be preferred in the situations when:
* Monolitica applications are used
* Consistent, long-running scenarious are in place
* In case if low-level OS/runtime installation/functions are needed
* Services, apps which require high availability

## EC2 Architecture
* ARM and Intel CPU machines are available for creating machines
* **Instance Store** volume can be attached to EC2 instance. It does not support Resilence. If it fails - data is lost. No replication for that type of volumes are supported. But it tends to be more fast then **EBS**.
* **Security Group** can be attached to network interface.
* Instance monitored using **CloudWatch**. By default instance provide metrics with __5 minutes__ interval. 
[EC2 Status Checs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html)

Instance state can be following:
* Running
* Stopped

Charges are only applied if instance is running. **Exept EBS** as it is network storage.
* [Instance States & Lifecycle](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html)

Some instances can **hibernate**:
* [AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Hibernate.html)

## Instance Types and Size
All instances can be split into families based on purpose of usage:
* General Purpose
    * **T2** and **T3**: Instances which allow burst capacity
    * **M5**: For general workloads
* Compute Optimized
    * **C4** More capable CPU
* Memory Optimized
    * **X1** and **R4** Optimize large amout of memory
* Storage Optimized
    * **I3** Delivers Fast IO
* Accelerated Computing
    * **P2**, **G3** and **F1**: Deliver GPU and FPGA

### Special cases
* "a": Used for AMD cpu
* "A": ARM Based
* "n": Higher speed networking
* "d": NVMe storage
### Links

* [Instance Types](https://aws.amazon.com/ec2/instance-types/)
* [Nitro Hypervisor](https://www.youtube.com/watch?v=e8DVmwj3OEs)

## EC2 Storage Architecture
Twor types of volumes can be used with instances:
* **Instance Store Volume** - attached directly to host (considered to be a temorary). Content survive reboot, but not start/stop.
[Instance Store Volumes](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)
* **EBS (Elastic Block Storage)** - is mount through the network. EBS replicates data inside AWS AZ.

### EBS Types
* **Mechanical(HDD)** **sc1** and **st1**
    * **sc1 (Cold Hdd)** Lowest cost, Infrequent access, can't be boot volume
        * Volume size is 500 GiB - 16 TB
        * Per-volume max throughput of 250 Mib/s and 250 IOPS
    * **st1** Low cost, througput intensive, can't be boot volume
        * Volume size is 500 GB - 16 TB
        * Used for frequently accessed, throughput-intensive workloads (streaming, big data)
* **SSD**
    * **gp2** Default, balance of IOPS/MiB/s. With **burst pool per GB**
        * 3 IOPS/GiB (100 IOPS - 16000 IOPS)
        * Bursts up to 3000 IOPS (credit based)
        * 1 GB - 16 TB size, max throughput per volume is 250 MiB/s
    * **io1** Highest performance, can adjust size and IOPS separately
        * User for applications which require sustained IOPS performzne
        * Large workloads
        * Volume size 4 GB - 16TB up to 64000 IOPS per volume (max for ssd volume)
        * Max throughput per volume is 1000 Mib/s

**EBS Snapshots** can be used in order to protect against AZ failure. Created snapshots can be **replicated** across AZ or Regions if needed.

**EBS** suppports a maximum per-instance throughput of **1750 MiB/S** and **80000 IOPS**. In case if that's not enough **Instance Store** considered to be used.
