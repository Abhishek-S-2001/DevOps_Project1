# DevOps_Project1
First trial project

Project Outline:

"""
Version Control with Git:

Initialize a Git repository for your project.
Create a simple HTML file (e.g., index.html) with some content.
Commit the HTML file to your Git repository.
Automation with Ansible:

Write an Ansible playbook to install Nginx on a remote server.
The playbook should copy your index.html file to the server.
Run the Ansible playbook to configure the server.
Infrastructure as Code with Terraform:

Write a Terraform script to provision an AWS EC2 instance.
Configure the instance to allow SSH access.
Use Ansible to provision the Nginx server on the EC2 instance.
Step-by-Step Guide:
1. Version Control with Git:

Copy code
# Initialize Git repository
git init

# Create index.html and add content
echo "<html><body><h1>Hello, DevOps!</h1></body></html>" > index.html

# Add and commit the changes
git add .
git commit -m "Initial commit with index.html"
2. Automation with Ansible:
Create a file named install_nginx.yml with the following content:

yaml

---
- name: Install Nginx
  hosts: your_target_server
  become: yes
  tasks:
    - name: Update package cache
      apt:
        update_cache: yes

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Copy index.html
      copy:
        src: /path/to/your/project/index.html
        dest: /var/www/html/index.html
Run the Ansible playbook:

bash

ansible-playbook install_nginx.yml -i "your_target_server,"

Replace your_target_server with the actual IP address or hostname of your target server.

3. Infrastructure as Code with Terraform:
Create a file named main.tf with the following content:

hcl

provider "aws" {
  region = "us-west-2"
}

resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  key_name      = "your_key_pair_name"

  tags = {
    Name = "web-server"
  }
}

resource "aws_security_group" "allow_ssh" {
  name        = "allow_ssh"
  description = "Allow SSH inbound traffic"
  
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

Run Terraform commands:

bash

terraform init
terraform apply

Replace your_key_pair_name with the name of your AWS key pair.

Now, update the Ansible playbook to use the public IP address of the EC2 instance as the target server, and run the playbook again.

This simple project will give you hands-on experience with Git, Ansible, and Terraform. Feel free to adapt and expand upon it as you explore more advanced features and scenarios!


"""
