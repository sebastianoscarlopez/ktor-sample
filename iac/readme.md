# Simple App Infrastructure

This repository contains the infrastructure setup for deploying a simple application on AWS using CloudFormation and GitHub Actions.

## Directory Structure

- `.github/workflows/deploy.yml`: GitHub Actions workflow for deploying the application.
- `ec2-instance.txt`: CloudFormation template for creating an EC2 instance for Docker deployment.
- `main-infrastructure.txt`: CloudFormation template for setting up the main infrastructure, including VPC, Subnet, Security Group, and ECR repository.

## Usage

1. Deploy the main infrastructure stack using the `main-infrastructure.txt` template.
2. Deploy the EC2 instance stack using the `ec2-instance.txt` template.
3. Trigger the GitHub Actions workflow to build and push the Docker image to ECR.

## CloudFormation Templates

### Main Infrastructure

The [main-infrastructure.txt](main-infrastructure.txt) template sets up the main infrastructure, including:
- VPC
- Internet Gateway
- Public Subnet
- Route Table and Route
- Security Group
- IAM Role and Instance Profile for EC2
- ECR Repository

### EC2 Instance

The [ec2-instance.txt](ec2-instance.txt) template creates an EC2 instance with the following properties:
- Instance type: `t2.micro`
- AMI ID: `ami-08970251d20e940b0`
- Key pair: `my-keypar`
- Subnet and Security Group imported from the main infrastructure stack
- User data script to install Docker and AWS CLI, and log in to ECR

## Deployment Workflow

The deployment workflow is defined in [deploy.yml](.github/workflows/deploy.yml). It performs the following steps:
1. Checks out the code.
2. Sets the Docker tag based on the provided app version.
3. Configures AWS credentials.
4. Logs in to Amazon ECR.
5. Builds the Docker image.
6. Tags the Docker image.
7. Pushes the Docker image to ECR.

## License

This project is licensed under the MIT License.