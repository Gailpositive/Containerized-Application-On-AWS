# Docker-Application-On-AWS
## Container-Basics

## PART 1: CREATING CONTAINER IN AWS
### AWS Technologies Used:
* AWS Identity and Access Management (IAM) policy and user (Policies and users are AWS account features, offered at no additional charge)
* AWS Cloud9 integrated development environment (IDE) instance
* AWS CloudFormation stack
* Amazon DynamoDB table


## PART 2: Create A Private Container Registry Within AWS Elastic Container Registry (ECR) and Deploy It On AWS App Runner
### AWS Technologis Used:
* AWS Cloud9 IDE
* AWS Identity and Access Management (IAM) policy and user 
* AWS App Runner service
* Amazon Elastic Container Registry (Amazon ECR) repository

  

### Setting up: Download Cloudformation template
* This exercise requires an IAM role that will be used with the AWS Cloud9 instance.
* It also requires a DynamoDB table that will be set up and then used in a later exercise.
* The CloudFormation stack will create these resources for you. You will also need to choose a Region where AWS App Runner is available: https://docs.aws.amazon.com/general/latest/gr/apprunner.html

* Download the following CloudFormation template: https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/DEV-AWS-MO-ContainersRedux/downloads/exercise-containers.yml (exercise-containers.yml.) This template will set up the backend resources that are needed to complete the exercise.


 ### Note: If there is an existing Virtual Private Cloud (VPC) and it has a Classless Inter-Domain Routing (CIDR) block of 10.16.0.0/16, you must edit the template to change it
* Download the following CloudFormation template. This template will set up the backend resources that are needed to complete the exercise.
* On AWS Management Console, open CloudFormation.
<img width="957" alt="1" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/2e1f19e0-c4e1-4e32-8857-90e7f5243beb">
* Create stack and tick templete
<img width="955" alt="2" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/15112954-6da8-4f6c-9805-9c92c6f566fc">
* For Specify template, choose Upload a template file.
<img width="958" alt="3a" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/a5e11039-c2df-4305-a9b5-7cfbefff9319">
* Choose file and browse to downloaded the exercise-containers template.
* Select the exercise-containers template and choose Open and Next.
<img width="929" alt="4" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/ac31e927-e5fb-4fa1-b732-81239d8e795b">
* For specify stack details, provide  Stack name, enter exercise-containers.
<img width="932" alt="5 stack created and named" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/ab6c56a7-801d-4c5a-8874-cec87a773b08">

* No tag was added
<img width="949" alt="6   click next" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/079e1f54-c78a-422b-b618-739e5fe2703d">

* Reviewed stack for any errors and corrections
<img width="944" alt="7 review" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/958fe762-bb11-430f-b687-7d9c4205ab46">
* Acknowledge Cloudformation to create IAM resources and submit stack 
<img width="946" alt="8 scroll down and acknowledge cloudformation and click next" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/39409f25-fa31-404d-a837-e58d30582672">

* Wait for the stack processing to complete
<img width="928" alt="9 stack in process" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/ce479254-a3e9-4f65-9af8-8809a844504e">
 
## PART 1: Creating the Container
### In this exercise, I will Switch over to Cloud9 Terminal to  create an instance and modify some of the environment settings,
### And install the prerequisites and source code that are needed to launch new container instances inside AWS Cloud9 environment.


### Task 1: Creating an AWS Cloud9 instance
* In the environment, give it a name
* Create an AWS Cloud9 instance
<img width="946" alt="10 create cloud9" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/19808089-f3ae-481f-87e7-e9c10f454ad7">
  
* In the Network setting, configure the following settings:
* Connection access: Aws system manager (SSM)
* Instance type: t3.small (2 GiB RAM + 2 vCPU) (I used t2 in this project)
* VPC settings: Containers VPC
* Choose Create.
<img width="960" alt="11 scroll down to setting choose vpc containers vpc" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/76dcc8b2-dc4d-4374-812b-dc07bd723f4f">
* Container successfully created in cloud9
 <img width="921" alt="12 container-cloud9 successfully created" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6468ee78-0e8f-45d6-815b-9df36709cb27"> 


### Task 2: Modify and deploy source code to AWS Cloud9
### In this task, I will upgrade the AWS Command Line Interface (AWS CLI) version  (https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
### 

* In the AWS Cloud9 terminal, I  upgrade the AWS CLI version
* Deploy the source code that’s needed to complete the exercise
* Associate the instance profile with my AWS Cloud9 instance
* Finally, I will expand my environment to give it more disk space.
<img width="910" alt="13aws install updated" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/0035dd75-30c6-4561-95ee-b07662ead032">

*  Verify the "AWS --version"
<img width="563" alt="14 very aws version" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/f1f69b3a-0258-4f9e-bcec-55e052ae4833">

* Download and extract the source code that I need for this exercise
<img width="927" alt="15 download and etract source code i need" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/575f1f2b-6a7b-42a8-9d16-82e78d824959">
  
* Replace the current association with the cloud9-containers-role.
<img width="749" alt="16 replacing aws association" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/453e0e6c-899b-4abe-b430-e019e43b91ec">

* Ensure that the State is listed as associated
<img width="655" alt="17 state is associated" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6a778ab0-af98-4a37-885c-d8a6fce0f531">

* To Update the environment for security measures,  specifically disable the managed rotated credentials, and instead use the cloud9-containers-IAM-role that CloudFormation created from the template
* The AWS security token services (sts) get-caller-identity command displays credential information delegated access to the IAM identity role used to authenticate the request
<img width="694" alt="18 aws get caller identity" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/3ed97f47-1952-4f64-9c41-31bf00adfc95">

* Expand the AWS Cloud9 disk specifically by running the a utility
<img width="705" alt="19 bash utilities c9-resize sh 40" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/0bad3db5-f2ae-49e0-89bf-71956a77100d">


### Task 3: Building the container
### In this task, I will pull the required images and build my Docker container.

* Cd to the container
<img width="835" alt="20b" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/89bea26d-c289-461b-b60b-b71451afe7dc">

* docker ls to view container created
<img width="748" alt="21 docker image created" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/4e39bd66-511f-4ab4-a13a-852013c56c74">

* docker run the container detach on port 8080
* docker ps view running docker containers
* Publish port 8080 to the Cloud9 host and make it available on port 8080.
<img width="753" alt="22 docker run d port 8080" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/adf268d2-2516-45ba-8d92-6558160f2945">

* View the application in a browser.
* At the top of my AWS Cloud9 instance, Preview and then choose Preview Running Application.
* View the running application.
<img width="941" alt="23 application running on browser" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/680d30f3-b84d-4801-95d0-1a60746f3e1b">

* Launch a shell inside the container
* docker exec -it webapp /bin/sh
* view process list
* In the container, view the contents of the /app folder and the contents of /app/input.txt.
* Escape out of the container
<img width="768" alt="24 docker exec" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/d914fe68-2539-4854-b2f1-29eb2f73bbe8">


* Stop and remove the running container.
<img width="764" alt="25 stop and rm running webapp" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/a18fe91b-7747-45a2-94d3-5262531de2ed">


### Task 4: Modifying the container with new data
* In this task, I will change the input.txt file inside the container with new data. I can use a bind mount to mount a local file resource in place of /app/input.txt inside the container.

* Create an ~/input.txt file with five words, with each word on a new line and 
* Launch a container with the new file mounted in place of /app/input.txt.
* Configure an application that’s running in a container with environment variables. The containerized application takes MESSAGE_COLOR as an environment variable.
<img width="737" alt="26  create app input text and launch a container with the new file mounted" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/77fdbb69-62ce-460d-8332-253e76a7a5ff">

* Visit the updated application in cloud9 browser by choosing Preview, Preview Running Application.
<img width="563" alt="27  view updated application running on broswer" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/cb65de88-b450-4287-9e2b-c3130d5b5327">

* Force-remove the container.
<img width="756" alt="28 Force remove the container" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/10de910a-37a5-4c7e-b4da-18c73e5fa671">



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
