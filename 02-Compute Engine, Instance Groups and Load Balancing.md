# Compute Engine

- When you need to deploy application in cloud, you'll need virtual servers. Google cloud provides Google Compute Engine (GCE) for the same.
- GCE helps in provisioning and managing virtual machines (virtual serves in GCP)
- GCE creates and manages lifecycle of Virtual Machine instances.
- It aids in load balancing and auto scaling multiple VM instances
- Manages network connectivity and configuration of VM instance.

## Install HTTP webserver on GCE VM

```
sudo su
apt update 
apt install apache2
ls /var/www/html
echo "Hello World!"
echo "Hello World!" > /var/www/html/index.html
echo $(hostname)
echo $(hostname -i)
echo "Hello World from $(hostname)"
echo "Hello World from $(hostname) $(hostname -i)"
echo "Hello world from $(hostname) $(hostname -i)" > /var/www/html/index.html
sudo service apache2 start
```

## Compute Engine VM IP Addresses

- **INTERNAL IP ADDRESS** :
    - Permanent internal IP Address that does not change during the lifetime of the instance
    - can only be used inside the specific network where the VM is created in
- **EXTERNAL OR EPHEMERAL IP ADDRESS** :
    - To be able to talk to the VM outside the network
    - IP address changes when instance is stopped
- **STATIC IP ADDRESS** :
    - Permanent external IP Address that can be attached to a VM
    - similar to Elastic IP Addresses in AWS

## Simplify webserver setup 

- How to reduce the number of steps required to create an VM instance and to set up Apache HTTP webserver?
    - Startup Script
    - Instance Template
    - Custom Image

- **using GCE STARTUP SCRIPT**

    STARTUP SCRIPT
    ```
    #!/bin/bash
    apt update 
    apt -y install apache2
    echo "Hello world from $(hostname) $(hostname -I)" > /var/www/html/index.html
    ```  
    - _**Bootstrapping**_ : Install OS patches or software when a VM instance is launched
    - In VM, you can configure Startup Script to bootstrap   

- **using Instance Template**
    - Need not specify VM instance details every time you launch an instance
    - This template is used in creating VM instances and managed instance groups
    - Define machine type, image, labels, startup scripts and other properties in the template
    - Template can't be updated

- **using Custom Image**
    - reduces launch time by creating a custom image with OS patches and software pre-installed
    - can be created from an instance, a persistent disk, a snapshot, another image or a file in Cloud Storage
    - can be shared across projects
    - Customize images to your corporate security standards - **Hardening an Image**

## Sustained use discounts in GCP

- to keep the cost of VM low
- Automatic discounts for running VM instances for significant portion of the billing month
- Discount increases with usage
- Applicable for instances created by Google Kubernetes Engines and Compute Engine
- **LIMITATIONS** :
    - does not apply on certain machine types (E2 and A2)
    - does not apply to VMs created by App Engine flexible and Dataflow

## Committed use discounts in GCP

- for workloads with predicted resource needs
- commit for 1 year or 3 year
- up to 80% discount based on machine type and GPUs
- applicable for instances created by Google Kubernetes Engine and Compute Engine
- cannot cancel commitments
- reach out to CLoud Biling Support if you made a mistake while purchasing commitments

## Preemptible VM 

- similar to spot instances in AWS
- short lived cheaper compute instances 
    - Max runtime for Preemptible VM : 24 hrs
    - can be stopped by GCP within 24 hrs
    - get 30 secs warning to save anything before terminating
- use this when
    - applications are fault tolerant
    - cost sensitive
    - workload not immediate
    - Example : Non immediate batch processing jobs
- _**LIMITATIONS**_ :
    - not always available 
    - no SLA by GCP
    - can't migrate to regular VMs
    - no automatic restarts
    - free tier credits not applicable    
- _**SPOT VMs**_ :
    - latest version of preemptible Vms
    - does not have maximum runtime (diff from preemptible VM)
    - dynamic pricing : 60-91% discount 

## Sole tenant Nodes (create VMs on dedicated host)

- Shared tenancy - single host machine can have instances from mulitple customers
- Sole-tenant Nodes - Virtualized instances on hardware dedicated to one customer
- **_USE CASES_** :
    - Security and compliance requirements : VMs to be physically seperated from those in other projects
    - High performance requirements : Group your VMs together
    - Licensing requirements : Using per-core or per-processor "bring your own licenses"

## Custom machine types

- when predefined options for Vms are not appropriate for your workload
- Machine types: E2, N2 or N1 
- Support a wide variety of OS : CentOs, CoreOs, Debian, red hat, Ubuntu, Windows
- Billed per vCPUs, memory provisoned to each instance

## GCE - VM costs

- 2 primary costs :
    - Infrastructure cost 
    - Licensing cost for OS - premium images only
        - examples of premium images : Red Hat enterprise linux, SUSE linux Enterprise Server, ubuntu pro
        - options for licensing: 
            - pay as you go model
            - use existing license with lot of constraints
- if existing license for a premium image exists use it and then shift to pay as you go model

# Instance Groups

- group of VM instances managed as a single entity
- _**TYPES**_:
    - Managed : 
        - identical VMs created using a template
        - features: auto scaling, auto healing and managed relases
    - Unmanaged :
        - different config for VMs in same group
        - does not offer auto scaling, auto healing and other services
        - not recommended unless you need different kinds of VMs
- Location can be zonal or regional but regional gives you higher availablity

## Managed Instance Groups

- Identical VM cretaed using an instance template
- _**FEATURES**_ :
    - Maintain certain number of instances - when an instance crashes, MIG launches another instance
    - Detect application failure using health checks (Self Healing)
    - Increase and decrease instances based on load (Auto healing)
    - Add load balancer to distribute load
    - Create instances in multiple zones (higher availabilty)
    - Release new application versions without downtime
        - Rolling updates - release new version step by step
        - Canary deployment - test new version with a group of instances before releasing it across all instances

## Creating Managed Instances

- Instance template is mandatory
- configure auto scaling:
    - Minimum number of instances
    - Maximum number of instances
    - Autoscaling metrics
        - Cool-down period
        - Scale in controls
        - CPU utilization target
    - Autohealing

# Load Balancing

- Distribute traffic across VM instances in one or more regions
- _**MANAGED SERVICES**_:
    - highly available
    - handles huge loads
    - LB can be private or public
- _**TYPES**_
    - External HTTP
    - Internal HTTP
    - SSL Proxy
    - TCP proxy
    - External network TCP/UDP
    - Internal TCP/UDP

