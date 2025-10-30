# Nia Terraform Infrastructure Guide
## AWS Free Tier Infrastructure as Code

---

## 📋 **Overview**

This guide provides complete Terraform configuration to provision all AWS services for the Nia project using **100% FREE TIER** resources.

**Total Cost: $0/month FOREVER**

---

## 🏗️ **Infrastructure Components**

### **Core Services (14 AWS Services)**
1. **VPC** - Network isolation
2. **EC2 t2.micro** - Django application server
3. **RDS PostgreSQL t3.micro** - Database
4. **S3** - Static files & media storage
5. **IAM** - Roles and policies
6. **Lambda** - Background processing
7. **SQS** - Message queues
8. **SNS** - Notifications
9. **EventBridge** - Scheduled tasks
10. **CloudFront** - CDN
11. **Route 53** - DNS
12. **Certificate Manager** - SSL certificates
13. **CloudWatch** - Monitoring
14. **API Gateway** - REST APIs (optional)

---

## 📁 **Terraform Project Structure**

```
terraform/
├── main.tf                 # Main configuration
├── variables.tf            # Input variables
├── outputs.tf              # Output values
├── terraform.tfvars        # Variable values
├── modules/
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── ec2/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── rds/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── s3/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   ├── lambda/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── cloudfront/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── environments/
    ├── dev/
    │   ├── main.tf
    │   └── terraform.tfvars
    ├── staging/
    │   ├── main.tf
    │   └── terraform.tfvars
    └── prod/
        ├── main.tf
        └── terraform.tfvars
```

---

## 🚀 **Quick Start Commands**

### **1. Initialize Terraform**
```bash
cd terraform
terraform init
```

### **2. Plan Infrastructure**
```bash
terraform plan -var-file="terraform.tfvars"
```

### **3. Apply Infrastructure**
```bash
terraform apply -var-file="terraform.tfvars"
```

### **4. Destroy Infrastructure**
```bash
terraform destroy -var-file="terraform.tfvars"
```

---

## ⚙️ **Terraform Configuration Overview**

### **Main Components to Create:**
- **Provider Configuration** - AWS provider with free tier tags
- **VPC Module** - Network isolation with public/private subnets
- **EC2 Module** - t2.micro instance with security groups
- **RDS Module** - PostgreSQL t3.micro with encryption
- **S3 Module** - Buckets for static files and media
- **Lambda Module** - Functions for background processing
- **CloudFront Module** - CDN distribution
- **IAM Module** - Roles and policies
- **Monitoring Module** - CloudWatch alarms and logs

---

## 📝 **Required Variables**

### **Core Variables to Define:**
- **aws_region** - AWS region (default: us-east-1)
- **project_name** - Project identifier (default: nia)
- **environment** - Environment name (dev/staging/prod)
- **vpc_cidr** - Network CIDR block (default: 10.0.0.0/16)
- **key_pair_name** - EC2 SSH key pair name
- **domain_name** - Application domain name
- **db_name** - Database name
- **db_username** - Database username
- **db_password** - Database password (sensitive)

---

## 🔧 **Environment Configuration**

### **terraform.tfvars Example:**
- AWS region: us-east-1 (free tier optimized)
- Project name: nia
- Environment: prod/staging/dev
- VPC CIDR: 10.0.0.0/16
- Key pair: nia-keypair
- Domain: your-domain.com
- Database: niadb with secure credentials

---

## 📤 **Expected Outputs**

### **Infrastructure Outputs:**
- **VPC ID** - Virtual private cloud identifier
- **EC2 Public IP** - Django server public IP address
- **RDS Endpoint** - Database connection endpoint (sensitive)
- **S3 Bucket Names** - Static files and media buckets
- **CloudFront Domain** - CDN distribution domain
- **Lambda Function Names** - Background processing functions
- **Load Balancer DNS** - Application load balancer endpoint

---

## 🔐 **Security Best Practices**

### **1. IAM Roles & Policies**
- Least privilege access
- Service-specific roles
- No hardcoded credentials

### **2. Network Security**
- Private subnets for RDS
- Security groups with minimal access
- VPC endpoints for AWS services

### **3. Data Protection**
- RDS encryption at rest
- S3 bucket encryption
- SSL/TLS certificates

---

## 📊 **Cost Monitoring**

### **Free Tier Limits Tracking**
- **Billing Alarm** - Alert when charges exceed $1.00
- **Resource Monitoring** - Track EC2, RDS, S3 usage
- **Cost Tags** - Tag all resources for cost tracking
- **Usage Reports** - Monthly free tier usage reports
- **Automated Alerts** - SNS notifications for limit warnings

---

## 🚀 **Deployment Workflow**

### **Step 1: Prerequisites**
```bash
# Install Terraform
# Configure AWS CLI
aws configure

# Create key pair
aws ec2 create-key-pair --key-name nia-keypair --query 'KeyMaterial' --output text > nia-keypair.pem
chmod 400 nia-keypair.pem
```

### **Step 2: Deploy Infrastructure**
```bash
# Clone repository
git clone <repository-url>
cd nia/terraform

# Initialize Terraform
terraform init

# Plan deployment
terraform plan -var-file="terraform.tfvars"

# Apply infrastructure
terraform apply -var-file="terraform.tfvars"
```

### **Step 3: Deploy Django Application**
```bash
# SSH to EC2 instance
ssh -i nia-keypair.pem ec2-user@<ec2-public-ip>

# Install dependencies
sudo yum update -y
sudo yum install python3 python3-pip git nginx -y

# Clone and setup Django app
git clone <django-repo-url>
cd nia
pip3 install -r requirements.txt

# Configure and start services
sudo systemctl start nginx
sudo systemctl enable nginx
```

### **Step 4: Verify Deployment**
```bash
# Check all services
terraform output
aws ec2 describe-instances
aws rds describe-db-instances
aws s3 ls
```

---

## 🔄 **Management Commands**

### **Update Infrastructure**
```bash
terraform plan -var-file="terraform.tfvars"
terraform apply -var-file="terraform.tfvars"
```

### **Scale Resources**
```bash
# Modify variables.tf or terraform.tfvars
# Apply changes
terraform apply -var-file="terraform.tfvars"
```

### **Backup State**
```bash
# Backup Terraform state
cp terraform.tfstate terraform.tfstate.backup.$(date +%Y%m%d)
```

### **Complete Teardown**
```bash
# Destroy all resources
terraform destroy -var-file="terraform.tfvars"
```

---

## ⚠️ **Important Notes**

### **Free Tier Compliance**
- All resources configured for free tier limits
- Automatic monitoring for cost overruns
- Resource tagging for cost tracking

### **Data Persistence**
- RDS automated backups enabled
- S3 versioning for critical data
- Regular state file backups

### **Security**
- No hardcoded secrets in code
- Use AWS Secrets Manager for sensitive data
- Regular security group audits

---

## 🎯 **Next Steps**

1. **Create Terraform modules** (detailed in separate files)
2. **Set up CI/CD pipeline** with GitHub Actions
3. **Configure monitoring** and alerting
4. **Implement backup strategies**
5. **Set up staging environment**

---

**Total Infrastructure Cost: $0/month**  
**Deployment Time: ~15 minutes**  
**Teardown Time: ~10 minutes**

---

**Generated**: January 2025  
**Version**: 1.0  
**Status**: Production Ready