# Docker-Application-On-AWS
## Container-Basics


# READINGS
## What is a container?
Containers provide a standard way to package your application's code, configurations, and dependencies into a single object. Containers share an operating system that's installed on the server. They run as resource-isolated processes, and are designed to provide quick, reliable, and consistent deployments—regardless of environment. For more information about containers and their benefits, see https://aws.amazon.com/getting-started/deep-dive-containers/#:~:text=Containers%20provide%20a%20standard%20way,consistent%20deployments%2C%20regardless%20of%20environment.

### Namespaces and cgroups
With containers, you can isolate processes from each other, which is a key component of how containers work. For more information about how namespaces and control groups (cgroups) work with containers, see on the NGINX blog.
https://www.nginx.com/blog/what-are-namespaces-cgroups-how-do-they-work/

### OCI
In this course, we mostly talk about using Docker containers. However, in 2015, Docker and other industry leaders came together to form the Open Container Initiative (OCI). The purpose of the OCI is to create standards for container formats and runtimes. For more information about the OCI, see https://opencontainers.org/about/overview/
About the Open Container Initiative

### Docker documentation
For more information about Docker, see the https://docs.docker.com/

### Benefits of containers
* Optimization of resource utilization:  You can fit multiple, lightweight containers on a single virtual machine, and increase the efficiency and density of your resources.
* Automation: The standard packaging and interaction with containers can make it easier to automate software development lifecycle tasks, such as building, deploying, and scaling applications.
* Speed: Containers are quick to run. You can start, scale, or delete containers in seconds.
* Scalability: Because containers facilitate microservices architectures, you can meet demand by using containers to scale out horizontally both quickly and efficiently.
* Increased developer productivity: 
* Developers can spend less time on operations and environment debugging, and spend more time on application development.
* Code portability: Having confidence that your workload will behave consistently across environments is one of the major benefits of containers.

For more information about the benefits and use cases for using containers on AWS, see https://aws.amazon.com/containers/

## What is the Docker daemon?
The Docker daemon runs on a host and listens for API calls to manage Docker objects. For example, if you want to build an image, run a container, or create a volume, you can use the Docker command line interface (CLI) to create the request.
 The request will then be submitted to the Docker daemon to be managed.

### What is the Docker CLI?
The Docker command line interface (CLI) is the client interface for interacting with Docker objects. The Docker CLI is how you issue commands to Docker to build your containers, run your containers, or stop your containers.

### What is a Dockerfile?
A Dockerfile is a text document that contains instructions on how to build your container image. A Dockerfile includes instructions for what base layer to use (for example, whether you want to use a minimal version of Linux or use an image that has preinstalled software, such as a database engine). Other instructions include running commands in the container, or copying your application data, dependencies, and configurations into the container. 
For more information,see https://docs.docker.com/develop/develop-images/dockerfile_best-practices/

### What is a Docker image?
A container image is created when you run the build command from the Docker CLI and it follows the instructions in a Dockerfile. A container image is made up of a series of read-only layers, with one writable layer on top where files can be added, modified, or deleted.
 Each layer is created from an instruction in the Dockerfile. 

### What is an image registry?
An image registry is a repository where you can store container images. You can store the images either publicly or privately. From the repository, images can be pulled and deployed, or used by other developers. 

### How do I store data in my container?
For more information about how to store data with Docker containers, see https://docs.docker.com/storage/



### BENEFITS OF DOCKER




### What are the contents of a Dockerfile?
The Dockerfile example that’s used in the demonstration uses the following instructions. These instructions were used as a good starting point for learning. For more information about Dockerfile instructions, see 
Dockerfile reference: https://docs.docker.com/engine/reference/builder/


### FROM: Defines the base image. All the instructions that follow are run in a container launched from the base image.

### WORKDIR: Sets the working directory for the subsequence instructions.

### ENV: Sets environment variables.

### COPY: Copies files and directories into the container image.

### RUN: Runs commands in the new container. This instruction commits a new layer on top of the present layer.

### CMD: Sets the default command to run when the container is launched.

### EXPOSE: Is used to document the containers that the port exposes.

### Docker commands
For more information, see the full reference for the docker base command: https://docs.docker.com/engine/reference/commandline/docker/
.

### docker build: Builds an image from a Dockerfile. In the demonstration, we pass -t to tag the image that’s created.

### docker run: Creates and starts a container. In the demonstration, we use -p to expose ports, -e to set environment variables, and -v to bind mount volumes.

### docker exec: Runs a command in a running container.

### docker stop: Stops a container.

### docker rm: Removes a container. Use -f to force the remove.


## PART 2: What is an image registry?
An image registry is a repository where you can store container images. From this registry, both DevOps tools and people can pull down container images to run, deploy, or expand on. Image registries can be public or private. Public registries are useful for providing images that can be used as base images for software development. For example, if your company provided a database engine, you could host images with the database software preinstalled on it. Your customers could then use these images as base images to expand on, which would make it easier for them to get their software up and running. Private registries are useful in situations where you don’t want to expose container images to the public, which is often the case with proprietary software.

## Docker Hub
Docker Hub is a popular repository for container images. It offers a variety of sources for container images that you can use, including images from container community developers, open-source projects, and software vendors. For more information about Docker Hub, see https://www.docker.com/products/docker-hub/
Docker Hub


## Amazon ECR
Amazon Elastic Container Registry (Amazon ECR) is a private, container image registry. With Amazon ECR, you can create multiple repositories to store and share your container images. To make it easier to deploy your containerized application, Amazon ECR integrates with other AWS services—such as Amazon Elastic Container Service (Amazon ECS), Amazon Elastic Kubernetes Service (Amazon EKS), and AWS Lambda.

## Amazon ECR Public
Amazon ECR also offers a highly available repository for your public images. You can create a repository for your authenticated AWS Identity and Access Management (IAM) identities to push to a public image repository. Thus, an unauthenticated user with or without an AWS account can pull from your public repository. For more information and to see a searchable list of public repositories, see the https://gallery.ecr.aws/
Amazon ECR Public Gallery


## AWS App Runner
AWS App Runner provides a way to run your containerized application on AWS infrastructure. You only need to supply a container image or application source to App Runner. App Runner creates all the infrastructure needed to host your application, and it also supplies you with an HTTP endpoint. App Runner serves your application with end-to-end encryption. As load increases, it will also scale within parameters that you define.



## AWS TECHNOLOGIES USED
AWS Identity and Access Management (IAM) policy and user 
AWS App Runner service
Amazon Elastic Container Registry (Amazon ECR) repository

### PART 2: Using Amazon ECR and AWS App Runner
* In this exercise, I create an Amazon ECR repository, authenticate to Amazon ECR, and then push my image to the Amazon ECR repository. I will then set up and deploy an AWS App Runner service.

### Task 1: Creating an Amazon ECR repository
* In this task, I will create an Amazon ECR repository.

1. In the AWS Management Console, choose Services, and then search for and open Elastic Container Registry.

2. If you have no existing repositories, choose Get Started. Otherwise, choose Create repository.

3. For Repository name, enter first-container and then choose Create repository.

4. Choose the first-container repository link and then choose View push commands.
* You should see the commands that you will use from your AWS Cloud9 instance.

### Task 2: Authenticate to Amazon ECR
* In this task, you will authenticate to Amazon ECR through the AWS Cloud9 IDE instance by running the push commands (which you saw in Amazon ECR).

1. In the AWS Management Console, choose Services, and then search for and open Cloud9.

2. Choose Open IDE.

3. In the AWS Cloud9 terminal, find the ACCOUNT_ID and the REGION, and insert these values into the aws ecr command.
* "export ACCOUNT_ID=$(aws sts get-caller-identity --output text --query Account)"
* "export REGION="`wget -q -O - http://169.254.169.254/latest/meta-data/placement/region`"
* "aws ecr get-login-password | docker login --username AWS --password-stdin ${ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com"

4. Add a new tag to first-container that references the Amazon ECR container registry.
* "docker tag first-container ${ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/first-container:latest"

  5. Push the image to Amazon ECR.
* "docker push ${ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/first-container:latest"

### Task 3: Setting up AWS App Runner
* In this task, you will set up and deploy an AWS App Runner service.
1. At the top left, choose the AWS Cloud9 icon and then choose Go To Your Dashboard.
2. In the AWS Management Console, choose Services, and then search for and open App Runner.
3. Choose Create an App Runner service.
4. For Container image URI, choose Browse.
5. Choose Image repository, choose first-container, and then choose Continue.
6. If you haven’t used Amazon ECR before, for ECR access role, choose Create new service role. Otherwise, you can keep Use existing service role selected.
7. Choose Next.
8. For Service name, enter first-container and choose Next.
9. Choose Create & deploy. Wait for the service creation to complete.
10. Choose the Default domain link.
* You should see the application running.

## Challenge
* You might recall that the containerized application takes MESSAGE_COLOR as an environment variable.
* For this challenge, edit your service settings and add an environment variable in the expected color format (for example, #0000ff).
* Wait for the service update to complete. Confirm the use of the environment variable by visiting the re-configured application.

## Cleaning up
* In this task, I delete some of the resources that I have used for this exercise.

!. Delete the AWS App Runner service.
* Open the App Runner dashboard.
* Choose first-container.
* Choose Actions and then choose Delete.
* Confirm the deletion.
2. Delete the IAM role.
* Open the IAM dashboard.
* Choose Roles.
* Delete AppRunnerECRAccessRole and confirm the deletion.
