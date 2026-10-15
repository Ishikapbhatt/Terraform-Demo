# Terraform AWS Infrastructure

This Terraform configuration creates the following AWS resources:

- **VPC**: Virtual Private Cloud with CIDR 10.0.0.0/16
- **Subnet**: Public subnet in us-east-1a with CIDR 10.0.1.0/24
- **Internet Gateway**: For internet access
- **Route Table**: Routes traffic to the internet gateway
- **Security Group**: Allows SSH (port 22) and HTTP (port 80) traffic
- **Key Pair**: Generates a new RSA key pair for SSH access
- **EC2 Instance**: t2.micro instance with Apache HTTP server serving a "Hello World" page

## Prerequisites

- AWS CLI configured with credentials
- Terraform installed

## Usage

1. Initialize Terraform:
```bash
terraform init
```

2. Review the plan:
```bash
terraform plan
```

3. Apply the configuration:
```bash
terraform apply
```

4. After deployment, the public IP of the EC2 instance will be displayed in the outputs. Access the hello world page at:
```
http://<public-ip>
```

5. SSH into the instance using the generated key:
```bash
ssh -i deployer-key.pem ec2-user@<public-ip>
```

## Cleanup

To destroy all resources:
```bash
terraform destroy
```

## Notes

- The key pair file `deployer-key.pem` will be generated in the current directory
- Make sure to keep the private key secure
- The AMI ID is for Amazon Linux 2 in us-east-1. You may need to update it for different regions
