# Cats and Dogs Cloud Application

Welcome to the Cats and Dogs Cloud Application repository! This project serves a static website that displays adorable images of cats and dogs. The application is containerized using Docker and hosted on AWS EC2 for easy deployment and scalability.

## Architecture

The application's architecture consists of the following components:

- GitHub: The source code for the Cats and Dogs application is stored in this GitHub repository.
- GitHub Actions: We have set up GitHub Actions to automatically build Docker images and push them to Amazon ECR whenever changes are merged into the master branch.
- Amazon ECR: Docker images of the Cats and Dogs application are securely stored in this container registry.
- AWS EC2: The containerized application is hosted on an EC2 instance, deployed in a public subnet of the default VPC for simplicity of debugging.

![project-2](https://github.com/patelrinkesh24/deploy-docker-container-on-Amazon-Linux-EC2/assets/50281621/3ec11942-66cb-46e5-9ec9-80cac8edd871)

## Getting Started

To get started with the Cats and Dogs Cloud Application, follow these steps:

### Prerequisites

1. Make sure you have Docker installed on your local development environment.
2. Create an AWS account and set up the necessary IAM permissions to interact with Amazon ECR and EC2.

### Local Development

1. Clone this repository to your local environment using the following command:

```
git clone https://github.com/yourusername/catsdogs-cloud9.git
cd catsdogs-cloud9
```

2. Build the Cats and Dogs Docker images locally:

```
docker build -t cats-app ./cats
docker build -t dogs-app ./dogs
```

3. Test the locally built images in your Cloud 9 environment:

```
docker run -d -p 8080:80 cats-app
docker run -d -p 8081:80 dogs-app
```

Open your browser and access the applications at `http://localhost:8080` for cats and `http://localhost:8081` for dogs.

### GitHub Actions Integration

1. Configure the GitHub repository settings to enable Docker image pushes to Amazon ECR. Make sure to securely store the AWS credentials in GitHub Secrets.

2. The GitHub Actions workflow defined in this repository will automatically build the Docker images and push them to Amazon ECR whenever changes are merged into the master branch.

### Deployment to AWS EC2

1. Deploy the necessary infrastructure using Terraform. We have provided Terraform code in a separate repository for creating Amazon ECR and EC2 instances.

```
# Clone the Terraform repository
git clone https://github.com/yourusername/terraform-ecr-ec2.git
cd terraform-ecr-ec2

# Initialize and apply Terraform
terraform init
terraform apply
```

2. Once the EC2 instance is up and running, log into the instance using SSH.

3. Log into Amazon ECR on the EC2 instance:

```
aws ecr get-login-password --region region | docker login --username AWS --password-stdin account-id.dkr.ecr.region.amazonaws.com
```

4. Pull the Cats and Dogs Docker images from Amazon ECR:

```
docker pull account-id.dkr.ecr.region.amazonaws.com/cats-app
docker pull account-id.dkr.ecr.region.amazonaws.com/dogs-app
```

5. Run the containers on EC2:

```
docker run -d -p 80:8080 account-id.dkr.ecr.region.amazonaws.com/cats-app
docker run -d -p 81:8080 account-id.dkr.ecr.region.amazonaws.com/dogs-app
```

Access the applications at `http://your-ec2-public-ip` for cats and `http://your-ec2-public-ip:81` for dogs.

## Updating the Application

To update the Cats and Dogs application, follow these steps:

1. Make the necessary changes to the application code in the respective directories (cats or dogs).

2. Commit and push the changes to the master branch of this GitHub repository.

3. GitHub Actions will automatically trigger a build of the updated Docker images and push them to Amazon ECR.

4. Log into the EC2 instance, pull the updated images, and redeploy the containers following the same steps as described in the "Deployment to AWS EC2" section.

## Frequently Asked Questions

1. **Why can we run two applications listening on the same port 80 on a single EC2 instance?**

   This is possible because each container runs in its isolated environment with its own network namespace. When mapping container port 80 to different host ports (e.g., 8080 and 8081), the traffic is directed to the respective containers based on the specified host port. The containers are kept separate and can run side by side without conflicts.

---

We hope you find this README helpful in understanding and using the Cats and Dogs Cloud Application. If you have any questions or encounter any issues, please feel free to open an issue in this repository.
