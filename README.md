# ansible-deploying-ec2
Ansible playbook for deploying ec2 instances
### Prerequisite:
1. Install Ansible on an ec2 Instance and setup it as Ansible-master
2. Python boto library
3. Create an AMI Role with Policy AmazonEC2FullAccess and attach it to the Ansible master instance.

##### vim ec2-deploy.yml

```sh
---
 - name: "ec2 instance creation"
   hosts: localhost
   tasks:
     - name: "Launching ec2 Instance"
       ec2:
        instance_type: t2.micro
        key_name: jwl-pc
        image: ami-0b898040803850657
        region: us-east-1
        group: webserver
        count: 1
        vpc_subnet_id: subnet-5074287e
        wait: yes
        assign_public_ip: yes
```
Change the values according to your needs.
---
```sh
  instance_type: t2.micro # Change the instance type according to your requirement
  key_name: jwl-pc # Select the key-pair which to be used
  image: ami-0b898040803850657 # Change it to your need(Currently using Amazon Linux)
  region: us-east-1 # Select Region
  group: webserver # Select Security group
  count: 1  # Count of the instances, you can deploy more than 1 instances
  vpc_subnet_id: subnet-5074287e  # VPC subnet
  wait: yes
  assign_public_ip: yes
```

###  run the playbook
```sh
ansible-playbook ec2-deploy.yml
```
