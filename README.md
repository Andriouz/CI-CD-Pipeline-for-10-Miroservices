**CI/CD | Deploy E-Commerce Website With 10 Microservices Using Multi-branch Pipeline Setup to Kubernetes Cluster**

![350531709-3a41fb69-1bd5-4a9a-b947-cbad24b0011e](https://github.com/user-attachments/assets/ba48231a-96c0-4091-9292-21853c41ae34)

**Why Microservices?**

Microservices is an architectural style where an application is built as a collection of small, independent services. Each service focuses on a specific business function and operates on its own. These services communicate with each other through well-defined APIs, making the system more modular and easier to manage.

**Project Overview**

**Project Name:** 11 Microservice CI/CD Pipeline

**Deployment Platform:** AWS EKS (Elastic Kubernetes Service)

**Application Type:** E-Commerce Website

**Microservices Overview**

The e-commerce platform is decomposed into the following 11 microservices:

1. **AdService:** Manages advertisements and promotions on the website.

2. **CartService:** Handles user shopping carts, including adding, removing, and updating items.

3. **CheckoutService:** Manages the checkout process, including order summary and confirmation.

4. **CurrencyService:** Provides currency conversion and pricing in different currencies.

5. **EmailService:** Sends confirmation and notification emails about purchases, promotions, and new products.

6. **Frontend:** Manages the website's user interface and user experience.

7. **External Frontend (for load balancing):** Distributes incoming traffic across multiple frontend instances to ensure high availability and performance.

8. **PaymentService:** Processes payments and handles transactions securely.

9. **ProductCatalogueService:** Manages product listings, details, and inventory.

10. **RecommendationService:** Provides product recommendations. Suggests products to users based on their browsing and purchase history.

11 **ShippingService:** Manages shipping logistics.


**Architecture and Technology Stack**

The deployment architecture leverages Kubernetes for container orchestration and Jenkins for CI/CD. Key components include:

- **Kubernetes Cluster:** Ensures scalable and reliable service deployment.

- **Jenkins:** Automates the build, test, and deployment process. Each microservice has its own Jenkinsfile defining the steps for building, testing, and deploying the service.

- **Docker:** Containerizes each microservice.

- **Helm:** Manages Kubernetes applications.

- **Prometheus and Grafana:** Monitoring and visualization tools.
  

**CI/CD Workflow**

1. **Code Commit:** Developers push changes to the Git repository.

2. **Branch Detection:** Jenkins Multibranch Pipeline detects new branches or commits.

3. **Build:** Jenkins builds the Docker image for the microservice. 

4. **Test:** Jenkins runs unit and integration tests.

5. **Push Image:** Jenkins pushes the Docker image to a container registry.

6. **Deploy:** Jenkins deploys the microservice to the Kubernetes cluster using Helm.

7. **Monitor:** The deployed microservice is monitored using Prometheus and Grafana.

**Hands-On Implementation Steps**

Phase 1: Infrastructure Setup

**1. Create a User in AWS IAM: Create a new user with any name.**

**2.Attach Policies: Attach the following policies to the newly created user:**

AmazonEC2FullAccess

AmazonEKS_CNI_Policy

AmazonEKSClusterPolicy

AmazonEKSWorkerNodePolicy

AWSCloudFormationFullAccess

IAMFullAccess

**3. Create an Inline Policy: Create an inline policy with the following content and attach it to your user:**

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "VisualEditor0",
      "Effect": "Allow",
      "Action": "eks:*",
      "Resource": "*"
    }
  ]
}
```

**4. Generate Secret Access Key: Once the IAM user is created, generate its Secret Access Key and download the credentials.csv file.**

**Launch Virtual Machine Using AWS EC2**

**1. EC2 Instance Requirements and Setup:**

**Instance Type:** t2.large
**vCPUs:** 2
**Memory:** 8 GB
**Network Performance:** Moderate
**Amazon Machine Image (AMI):** Ubuntu Server 20.04 LTS (Focal Fossa)
**Security Groups:** Security groups act as a virtual firewall for your instance to control inbound and outbound traffic.

- Port 22 (SSH): Allows SSH access to the instance.
  
- Port 80 (HTTP): Allows web traffic to the instance.
  
- Port 465 (SMTP): Used for secure email transmission.
  
- Port 3000: Commonly used for development servers (e.g., Node.js).
  
- Port 8080: Often used for web servers and development.
  
- Port 8081: Another common port for web servers.
  
- Port 9090: Typically used for web-based management interfaces.
  
- Port 9000: Often used for custom applications.
  
- Port 32630: Specific to your application needs.
  
- Port 6443: Kubernetes API server.
  
- Port 9115: Prometheus metrics.

- Outbound Rules: Allow all traffic to ensure the instance can communicate externally.
  
**2. SSH into the Server: After launching your virtual machine, Open your terminal and use the following command to SSH into your instance:**
  
ssh -i /path/to/your-key-pair.pem ubuntu@your-ec2-public-dns

Replace /path/to/your-key-pair.pem with the path to your key pair file and your-ec2-public-dns with the public DNS of your EC2 instance.


