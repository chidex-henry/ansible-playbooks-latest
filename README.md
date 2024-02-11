## Project: Deploying a Static Website on AWS with Ansible

### Overview
This project demonstrates the deployment of a static website on AWS using Ansible and AWS EC2 instances. Ansible, a robust IT automation system, facilitates configuration management, application deployment, cloud provisioning, ad-hoc task execution, network automation, and multi-node orchestration. The project utilizes a reference architecture to construct a three-tier AWS network VPC from scratch. Key AWS services deployed include VPC, subnets, NAT gateways, Security Groups, EC2 Instance connect endpoint, ALB, and Route 53.

<img width="540" alt="image" src="https://github.com/chidex-henry/ansible-playbooks-latest/assets/77998377/1d983f10-c749-482f-a369-51e90d7e6f3e">


### Reference Architecture Summary

1. **Virtual Private Cloud (VPC) Configuration**:
    - Created VPC with public and private subnets across two availability zones.
    - Deployed an Internet Gateway for connectivity between VPC instances and the Internet.
    - Implemented Security Groups for network firewall management.

2. **High Availability and Fault Tolerance**:
    - Utilized two Availability Zones for enhanced reliability.
    - Positioned infrastructure components strategically across public and private subnets.

3. **EC2 Instance Configuration**:
    - Employed EC2 Instance Connect Endpoint for secure connections.
    - Hosted the website on EC2 instances placed within private subnets.
    - Enabled internet access for instances in private subnets via NAT Gateway.

4. **Deployment with Ansible**:
    - Configured an Ansible server in the private subnet.
    - Launched EC2 instances named webservers across different regions.
    - Tested connectivity between Ansible server and webservers using keypairs.
    - Stored Ansible Playbooks on GitHub for configuration management.
    - Created Ansible Inventory file to manage nodes.
    - Deployed web setup from Ansible server to webservers using Ansible Playbooks.

5. **Additional Features**:
    - Utilized Application Load Balancer for traffic distribution.
    - Implemented Auto Scaling Group for managing EC2 instances.
    - Secured application communications with Certificate Manager.
    - Configured Simple Notification Service (SNS) for Auto Scaling Group alerts.
    - Registered domain name and set up DNS record with Route 53.

### Commands Used

- **Test Connection Between Ansible Server and Web Servers**:
    - `sudo yum update -y`
    - `sudo yum -y install python-pip`
    - `sudo pip install boto3`

- **Install Ansible on Ansible Server**:
    - `sudo apt update`
    - `sudo apt upgrade`
    - `sudo apt install software-properties-common -y`
    - `sudo apt install ansible -y`
    - `ansible –version`

- **Create Ansible Inventory File**:
    ```
    [all:vars]
    ansible_python_interpreter=/usr/bin/python2.7
    ```

- **Use Ansible to Ping Web Servers to Test Connection**:
    ```
    ansible all --key-file ~/.ssh/id_rsa -i inventory -m ping -u ec2-user
    ansible all -m ping
    ```

- **Jupiter Website Commands Setup**:
    - Script for Ansible Playbook commands to deploy the website.

     #!/bin/bash: This line indicates that the script should be executed using the Bash shell.

    sudo su: Switches the user to the superuser or root user for executing subsequent commands with elevated privileges.

    yum update -y: Updates the package manager and all installed packages without prompting for confirmation (-y flag).

    yum install -y httpd: Installs the Apache HTTP server (httpd) package without prompting for confirmation.

    cd /var/www/html: Changes the current directory to /var/www/html, which is the default web root directory for Apache.

    wget https://github.com/azeezsalu/jupiter/archive/refs/heads/main.zip: Downloads the main.zip file from the specified GitHub repository.

    unzip main.zip: Unzips the downloaded main.zip file, extracting its contents.

    cp -r jupiter-main/* /var/www/html/: Copies the contents of the extracted jupiter-main directory to the Apache web root directory.

    rm -rf jupiter-main main.zip: Removes the jupiter-main directory and the main.zip file to clean up after the deployment.
  
    systemctl enable httpd: Enables the Apache HTTP server to start automatically upon system boot.

    systemctl start httpd: Starts the Apache HTTP server immediately.
  

### Conclusion
By following this setup, users can effectively deploy a static website on AWS using Ansible, leveraging automation and infrastructure as code principles for efficient management and scalability. This comprehensive approach ensures robustness, reliability, and ease of maintenance in hosting static web content on AWS infrastructure.
