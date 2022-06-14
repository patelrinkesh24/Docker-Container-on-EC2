# assignment-1
<h2>Create Dockerfile, build docker image and deploy docker container on Amazon Linux EC2</h2> 

![Cats and Dogs - Page 3 (1)](https://user-images.githubusercontent.com/50281621/173474517-75777b08-7658-427b-b266-7f04e5675426.png)

In this project, Terraform code was used to deploy the architecture for creating Virtual Private Cloud, Internet Gateway and a Public Subnet. Amazon EC2 and ECR were also deployed using this Terraform Code. Additionally, Github Actions was written to deploy the images into Amazon Elastic Container Registry (ECR).

Under EC2, two Docker images were created on Linux OS. Each images will be used to publish static website hosting cats and dogs images pushed to ECR using github Actions. 
