# Task_10_

Implement Blue/Green Deployment for Strapi App using GitHub Actions CI/CD
Below are the steps which I performed: 

1. Containerization & Image Push
   
- I Used an existing Dockerized Strapi application.

- Then tagged and pushed the Docker image to Amazon ECR

2. Terraform-Based ECS Infrastructure
   
- Created the following Terraform resources:

- VPC, Subnets, Security Groups

- ALB (Application Load Balancer) with:

- Two Target Groups: strapi-blue-tg and strapi-green-tg

- Listener on port 80 forwarding to the target group

- ECS Cluster and Fargate Task Definition using the ECR image

- ECS Service with:

- Blue/Green deployment support

- Linked to both target groups

- ECS Cluster Capacity Providers (FARGATE_SPOT + FARGATE)

- Deployment Controller set to "CODE_DEPLOY"

3. CodeDeploy Configuration
   
 Created:
 
- CodeDeploy Application for ECS

- CodeDeploy Deployment Group with:

- Blue/Green deployment strategy (CodeDeployDefault.ECSCanary10Percent5Minutes)

- Traffic shifting between target groups

- Auto rollback and termination of original task set after deployment

4. GitHub Actions CI/CD Setup
   
- Configured .github/workflows/terraform_task10.yml which performed:

- Checkout code
- Initialize and apply Terraform

- Trigger CodeDeploy deployment using AWS CLI

5. Manual Verification
   
- Accessed Strapi app via ALB DNS URL.

- Verified deployment success in CodeDeploy console:

- Canary deployment (10% → 100% traffic shift)

- Replacement task set successfully took over

- Original task set terminated post-wait

6. Results
   
- Blue/Green deployment completed successfully.

- Zero downtime with automatic traffic shifting.

- Infrastructure automated and managed using Terraform.

- Deployment triggered through GitHub Actions and verified on AWS Console.



![image](https://github.com/user-attachments/assets/f6d356be-0252-44c4-84be-e5d331442256)

![image](https://github.com/user-attachments/assets/3701b23e-e8b4-4b20-9a2d-8de125d39a00)

![image](https://github.com/user-attachments/assets/1e115d64-bb92-4a59-8a7f-26abf8b1da98)

![image](https://github.com/user-attachments/assets/a01557df-8bb1-426c-89cd-e29945e36759)









