# CloudLaunch-AltSchool
AltSchool Semester 3 month 1 Cloud Engineering Assignment
README.md — AltSchool Cloud Assignment 1
# CloudLaunch Project – AltSchool Cloud Engineering

Submission Checklist

 README.md with:

Description of Task 1 and Task 2.

S3 site link.

Optional CloudFront URL.

IAM JSON policy attached to cloudlaunch-user.

AWS account ID / console URL / username.

 Screenshots:

S3 buckets + website + CloudFront.

IAM user & policy.

VPC layout (subnets, route tables, security groups).

 GitHub repo:

Include README.md, index.html, style.css, IAM-policy.json.

 Optional bonus: CloudFront URL linked in README.





 
## 📝 Overview
This project demonstrates the setup of a **secure and structured AWS environment** using VPC, subnets, security groups, and S3 static website hosting.  
It covers **Task 1** (S3 Static Site) and **Task 2** (VPC Design, Route Tables, Security Groups, and IAM Access).

---




## 🔹 Task 1: S3 Static Website
- **Bucket Name:** `cloudlaunch-site-bucket-brown`  
- **Purpose:** Host a static landing page for CloudLaunch.  
- **Test Page:** `index.html` with custom styling (`style.css`) displaying a modern landing page.  
- **Website Endpoint:** [Static Site Link](http://cloudlaunch-site-bucket-brown.s3-website-eu-west-1.amazonaws.com/))  
- **Optional CloudFront URL:**(bonus task).  

**Steps Performed:**  
1. Created an S3 bucket.  
2. Uploaded `index.html` and `style.css`.  
3. Enabled static website hosting in bucket properties.  
4. Configured bucket policy to allow public read access.  
5. Verified the website loads successfully in browser.

### CloudFront Distribution (Optional Bonus)
- **Distribution Name:** cloudlaunch-distro
- **CloudFront URL:** https://de8jbppsfbdet.cloudfront.net
- **ARN:** arn:aws:cloudfront::311141558987:distribution/E1MCANY7YP9QJH
- **Purpose:** Serve the static site globally with CDN acceleration.
---






## 🔹 Task 2: VPC, Subnets, Route Tables & Security Groups

### VPC
- **Name:** `cloudlaunch-vpc`  
- **CIDR Block:** `10.0.0.0/16`  

### Subnets
| Subnet Name             | CIDR Block    | Type      |
|-------------------------|--------------|-----------|
| `cloudlaunch-public-subnet` | 10.0.1.0/24 | Public    |
| `cloudlaunch-app-subnet`    | 10.0.2.0/24 | Private   |
| `cloudlaunch-db-subnet`     | 10.0.3.0/28 | Private   |

### Route Tables
| Route Table Name        | Associated Subnet         | Notes                  |
|-------------------------|--------------------------|-----------------------|
| `cloudlaunch-public-rt` | `cloudlaunch-public-subnet` | Public route to Internet Gateway (0.0.0.0/0) |
| `cloudlaunch-app-rt`    | `cloudlaunch-app-subnet`    | Private, no internet route |
| `cloudlaunch-db-rt`     | `cloudlaunch-db-subnet`     | Private, no internet route |

### Security Groups
| Security Group Name      | Description                      | Inbound Rules                              |
|--------------------------|----------------------------------|-------------------------------------------|
| `cloudlaunch-app-sg`     | Allow HTTP within VPC only       | HTTP (80) from `10.0.0.0/16`             |
| `cloudlaunch-db-sg`      | Allow MySQL from App subnet only | MySQL/Aurora (3306) from `10.0.2.0/24`   |

### IAM User: `cloudlaunch-user`
- **Purpose:** Read-only testing of VPC, subnets, and security groups.  
- **Permissions:** JSON policy attached to allow only `Describe*` EC2/VPC actions (no create, modify, delete).  
- **Policy:**

  

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeVpcs",
                "ec2:DescribeSubnets",
                "ec2:DescribeRouteTables",
                "ec2:DescribeSecurityGroups",
                "ec2:DescribeInternetGateways",
                "ec2:DescribeNetworkAcls",
                "ec2:DescribeAccountAttributes",
                "ec2:DescribeDhcpOptions",
                "ec2:DescribeTags"
            ],
            "Resource": "*"
        }
    ]
}




User Credentials:

AWS Account ID / Alias: cloudlaunch-aws

Username: cloudlaunch-user

Password: Enforced to change on first login (ALT@2025)

Test Results: Successful

Can list VPC resources ✅

Cannot create, modify, or delete ❌




💡 Notes & Best Practices

Private subnets remain isolated with no 0.0.0.0/0 routes.

Security groups follow least privilege principle.

IAM user enforces role separation and safe testing.

Bucket policy and S3 public access configured correctly to serve static content.




✅ Status

 S3 static website working

 VPC and subnets created correctly

 Route tables associated correctly

 Security groups configured securely

 IAM user read-only verified
