# CS4843Assignment2
## Description:
Using AWS, creates a cloud infrastructure for a web application. 
### Technologies Used:
- YAML: Used to write the infrastructure as code.
- JSON: Used to write the parameters.

### Infrastructure:
AWS's Cloudformation was utilized to create the infrastructure.
Three YAML files are utilised to set up specific parts of the infrastructure:
- network.yaml:
    Creates:
    - A Virtual Private Cloud(VPC)
    - An internet gateway
    - Two Public and Two private subnets
    - A NAT gateway for each public subnet
- securityAndServers.yaml:
    Creates:
    - Two EC2 instances that run Apache Web Server.
    - An Elastic Load Balancer
    - Security Groups for the servers
- databaseAndStorage.yaml:
    Creates:
    - Two MySQL databases
    - Creates two EC2 Volumes

Infrastructure Layout:
AWS Region: US West (Oregon) us-west-2
- Virtual Private Cloud(VPC): CIDR = 10.0.0.0/16
    - First Availablility Zone:
        - Public Subnet 1: CIDR = 10.0.0.0/24
            - Nat Gateway 1: Allows Private Subnet 1 egress internet access
        - Private Subnet 1: CIDR = 10.0.2.0/16
            - Ec2 Instance: Runs Apache Web Server
            - Database Instance: Runs a MySQL database
    - Second Availablility Zone:
        - Public Subnet 2: CIDR = 10.0.1.0/16
            - Nat Gateway 1: Allows Private Subnet 1 egress internet access
        - Private Subnet 2: CIDR = 10.0.3.0/16
            - Ec2 Instance: Runs Apache Web Server
            - Database Instance: Runs a MySQL database

### Delpoying the Infrastructure:
In an AWS CLI, enter these commands one by one in the order given: 
Note: Before entering the commands, make sure your are in the same directory as the files.
1. aws cloudformation create-stack --stack-name network --template-body file://network.yaml --parameters file://networkParams.json
2. aws cloudformation create-stack --stack-name serversAndSecurity --template-body file://securityAndServers.yaml --parameters file://securityAndServersParams.json
3. aws cloudformation create-stack --stack-name databaseAndStorage --template-body file://databaseAndStorage.yaml --parameters file://databaseAndStorageParams.json
