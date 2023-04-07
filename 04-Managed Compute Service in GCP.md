# Managed Compute Services in GCP

- Compute Engine :
    - IaaS
    - Provision VMs to scale globally

- Google Kubernetes Engine :
    - CaaS
    - Orchestrate containerized microservices/ applications
    - Needs complex cluster configurations
    - Provides Pod and Cluster Autoscaling

- Google App Engine :
    - PaaS and serverless
    - Deploy applications in fully mananged platform
    - CaaS : If containers are used to run application (App Engine Flexible)
    - Serverless : If applications run in language specific sandboxes (App Engine Standard)

- Cloud Functions :
    - FaaS and serverless
    - event driven application
    - pay for use - pay only for no. of invocations
    - time bound

- Cloud Run :
    - CaaS and serverless
    - can't run DBs on it
    - not hosted within customer's VPC
    - can go down to 0 instances