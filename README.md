# A Practical Guide to EKS

In this repository you will find all the assets required for the course `A Practical Guide to Amazon EKS`, by A Cloud Guru.


## Bookstore application

This solution has been built for for explaining all the concepts in this course. It is complete enough for covering a real case of microservices running on EKS and integrating with other AWS Services.


## Project walkthrough on EC2 instance

# The Bookstore Project
# https://learn.acloud.guru/course/a-practical-guide-to-amazon-eks/learn/bfa1a3dc-659a-4bbc-b067-eed60129ed5f/ee0f2399-e73a-4373-8525-f8bc3aecb20e/watch

# Create an EC2 instance (Amazon Linux 2, t2.micro), use a security group that allows SSH, HTTP, and HTTPS traffic

# Connect to your EC2 instance

ssh -i /path/key-pair-name.pem ec2-user@<Public IPv4 address>

# Configure your AWS CLI

aws configure

AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-east-1
Default output format [None]: json

# Confirm connectivity to your AWS account

aws sts get-caller-identity
{
    "Account": "XXXXXXXXXXXX",
    "UserId": "AIDAWC4L6452CNEXAMPLE",
    "Arn": "arn:aws:iam::XXXXXXXXXXXX:user/cloud_user"
}

# Install git and Docker

sudo yum install git docker -y

# Configure and start Docker

sudo usermod -aG docker ec2-user

sudo systemctl enable docker

sudo systemctl start docker

# Log out and log back in to your EC2 instance, so that your group membership is re-evaluated

exit

ssh -i /path/key-pair-name.pem ec2-user@<Public IPv4 address>

# Install docker-compose

sudo pip3 install docker-compose

# From '/home/ec2-user/', clone the Course_Practical_Guide_EKS GitHub repository

git clone https://github.com/ACloudGuru-Resources/Course_Practical_Guide_EKS.git

# Create DynamoDB tables

chmod +x /home/ec2-user/Course_Practical_Guide_EKS/renting-api/infra/cloudformation/create-dynamodb-table.sh

cd /home/ec2-user/Course_Practical_Guide_EKS/renting-api/infra/cloudformation

./create-dynamodb-table.sh

# Expected output: "Successfully created/updated stack - development-renting-api-dynamodb-table"

chmod +x /home/ec2-user/Course_Practical_Guide_EKS/clients-api/infra/cloudformation/create-dynamodb-table.sh

cd /home/ec2-user/Course_Practical_Guide_EKS/clients-api/infra/cloudformation

./create-dynamodb-table.sh

# Expected output: "Successfully created/updated stack - development-clients-api-dynamodb-table"

chmod +x /home/ec2-user/Course_Practical_Guide_EKS/inventory-api/infra/cloudformation/create-dynamodb-table.sh

cd /home/ec2-user/Course_Practical_Guide_EKS/inventory-api/infra/cloudformation

./create-dynamodb-table.sh

# Expected output: "Successfully created/updated stack - development-inventory-api-dynamodb-table"

chmod +x /home/ec2-user/Course_Practical_Guide_EKS/resource-api/infra/cloudformation/create-dynamodb-table.sh

cd /home/ec2-user/Course_Practical_Guide_EKS/resource-api/infra/cloudformation

./create-dynamodb-table.sh

# Expected output: "Successfully created/updated stack - development-resource-api-dynamodb-table"

# Go back to your root folder

cd /home/ec2-user/Course_Practical_Guide_EKS

# Configure the '.env' file with your AWS credentials

vim .env

AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

:x

# Run docker-compose from your '/home/ec2-user/Course_Practical_Guide_EKS' folder

docker-compose up

# Retry the command above if the first attempt does not succeed

# Expected output:

inventory-api_1  | Inventory API Running...
renting-api_1    | => Booting Puma
renting-api_1    | => Rails 6.0.3.6 application starting in development
renting-api_1    | => Run `rails server --help` for more startup options
renting-api_1    | Puma starting in single mode...
renting-api_1    | * Version 4.3.7 (ruby 2.6.3-p62), codename: Mysterious Traveller
renting-api_1    | * Min threads: 5, max threads: 5
renting-api_1    | * Environment: development
renting-api_1    | * Listening on tcp://0.0.0.0:5004
renting-api_1    | Use Ctrl-C to stop

# Launch your application by typing the public IP address of your EC2 instance in a web browser

> You can find in [here](_docs/api.md) the documentation of the APIs.
