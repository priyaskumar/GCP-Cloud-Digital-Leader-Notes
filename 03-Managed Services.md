# Managed Services

- run applications in cloud the same way it is run in data center
- _**CLOUD SERVICES**_ :
    - Iaas
    - Paas
    - Faas
    - Caas
    - Serverless
    - Saas

## IAAS

- use only infrastructure (ONLY VM) to deploy applications or databases
- You're responsible for :
    - Application Code and Runtime
    - Configuring load balancing
    - Auto scaling
    - Os upgrades and patches
    - availability

## PAAS

- use platform provided by cloud
- You're responsible for :
    - Configuration
    - Application Code
- Cloud provider is responsible for :
    - OS
    - Application Runtime
    - Auto scaling, avalabilty and load balancing
- Types:
    - CAAS - Container as a Service - Container instead of Apps
    - FAAS - Function as a Service - Functions instead of Apps
    - DATABASES - Relational and NoSQL, Queues, AI, ML, Operations

## CAAS

### Microservices

- Enterprises are now using micriservices architecture
    - build small focused microservices
    - flexibilty to innovate 
- deployments become complex
- deployments can be done using Containers 

### Containers - DOCKER

- create docker image for each microservices
- docker image has :
    - application runtime
    - application code and dependencies
- runs same way on any infrastructure
- _**ADVANTAGES OF DOCKER**_ :
    - light weight
    - isolation for containers
    - cloud neutral

### Container Orchestration

- _**FEATURES**_:
    - Auto scaling
    - Service Discovery
    - Load Balancer
    - Self Healing
    - Zero downtime deployments

## Serverless

- No need to focus on server(infrastructure) rather focus on code 
- pay for use (zero requests - zero cost)
- cloud managed service takes care of all that is needed to scale your code to serve millions of requests

## SAAS 

- centrally hosted software 
- pay as you go
- You're responsible for :
    - Software Configuration
    - Content
- Cloud is responsible for:
    - OS
    - Application Runtime
    - Auto Scaling
    - Availabilty
    - Load Balancing
    - Application code
    - Application configuration

## Shared Responsibilty Model

- Security is a shared responsibilty of GCP and Customer
- You're responsible for :
    - SaaS : 
        - Content
        - Access Policies
        - Usage
    - PaaS :
        - SaaS
        - Deployment
        - Web application security
    - IaaS :
        - PaaS
        - Operations
        - Network Security
        - Guest OS
- GCP is responsible for :
    - Hardware
    - Network
    - Audit Logging
    - Encryption
    - IAM
    - KMS




