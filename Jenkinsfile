#!/bin/bash
set -xe

git clone https://github.com/Danish1790/Aws_Terraform.git
cd Aws_Terraform/Terraform

sed -i "s/server_name/${SERVER_NAME}/g" backend.tf
export TF_VAR_name=${SERVER_NAME}

terraform init
terraform plan
terraform $TERRAFORM_ACTION -auto-approve

//set time of 120 sec for ec2 instance to be created
sleep 125

if [ $TERRAFORM_ACTION = "destroy" ]; then
	exit 0
else
	cd ../Ansible
	ansible-playbook -i /opt/ansible/inventory/aws_ec2.yaml apache.yaml 
fi
