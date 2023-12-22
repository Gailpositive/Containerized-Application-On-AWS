# Containerized-Application-On-AWS
## Container-Basics

### Exercises-Course,I'll be create the following resources:
* AWS Identity and Access Management (IAM) policy and user (Policies and users are AWS account features, offered at no additional charge)
* AWS Cloud9 integrated development environment (IDE) instance
* AWS CloudFormation stack
* Amazon DynamoDB table

### Setting up
* This exercise requires an IAM role that will be used with the AWS Cloud9 instance.
* It also requires a DynamoDB table that will be set up and then used in a later exercise.
* The CloudFormation stack will create these resources for you. You will also need to choose a Region where AWS App Runner is available: https://docs.aws.amazon.com/general/latest/gr/apprunner.html

1. Download the following CloudFormation template: https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/DEV-AWS-MO-ContainersRedux/downloads/exercise-containers.yml (exercise-containers.yml.) This template will set up the backend resources that are needed to complete the exercise.
   
### Note: If you have an existing Virtual Private Cloud (VPC) and it has a Classless Inter-Domain Routing (CIDR) block of 10.16.0.0/16, you must edit the template to change it.

2. Sign in to the AWS Management Console as a user that has administrator permissions.

3. Choose Services, and search for and open CloudFormation.

4. Choose Create stack.

5. For Specify template, choose Upload a template file.

6. Select Choose file and browse to where you downloaded the exercise-containers template.

7. Select the exercise-containers template and choose Open.

8. Choose Next.

9. For Stack name, enter exercise-containers.

10. Choose Next, and then choose Next again.

11. Select the acknowledgement and choose Create stack. Wait for the stack to complete.

## Exercise 1: Creating the First Container
* In this exercise, you create an AWS Cloud9 instance and modify some of the environment settings. You also install the prerequisites and source code that are needed to launch new container instances inside your AWS Cloud9 environment.

### Task 1: Creating an AWS Cloud9 instance
* In this task, you will create an AWS Cloud9 instance.

!. In the AWS Management Console, choose Services, and then search for and open Cloud9.
2. Choose Create environment.
3. For Name, enter containers-cloud9 and choose Next step.
4. Configure the following settings:
 * Instance type: t3.small (2 GiB RAM + 2 vCPU)
 *Network settings: VPC settings: Containers VPC
5. Choose Create.

### Task 2: Modifying and deploying source code to AWS Cloud9
In this task, you will upgrade the AWS Command Line Interface (AWS CLI) version  https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html , and deploy the source code that’s needed to complete the exercise. You will also associate the instance profile with your AWS Cloud9 instance. Finally, you will expand your environment to give it more disk space.

1. In the AWS Cloud9 terminal, upgrade the AWS CLI version by running the following command.
* curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
* unzip awscliv2.zip
* sudo ./aws/install
* . ~/.bashrc
* 
2. Verify the version
* aws --version

3. Download and extract the source code that you need for this exercise.
* wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/DEV-AWS-MO-ContainersRedux/downloads/containers-src.zip
* unzip containers-src.zip
  
4. Replace the current association with the cloud9-containers-role.
* export ASSOC_ID="`aws ec2 describe-iam-instance-profile-associations | grep AssociationId | cut -f2- -d: | tr -d ',' | xargs`"
* aws ec2 replace-iam-instance-profile-association --iam-instance-profile Name=cloud9-containers-role --association-id $ASSOC_ID

5. Make sure that the State is listed as associated
* aws ec2 describe-iam-instance-profile-associations

6. Run the following command.
* This command tells AWS Cloud9 to specifically disable the managed rotated credentials, and instead use the cloud9-containers-role that CloudFormation created from the template.
* aws cloud9 update-environment  --environment-id $C9_PID --managed-credentials-action DISABLE

7. Wait for a couple of minutes, and then run the following command:
* aws sts get-caller-identity
* You should see an Amazon Resource Name (ARN) that matches a role in the CloudFormation template:
* arn:aws:sts::0123456789012:assumed-role/cloud9-containers-role/i-xxxxxxxxxxxxxxxxxx

8. Expand the AWS Cloud9 disk by running the following utility:
* bash utilities/c9-resize.sh 40

### Task 3: Building the first container
* In this task, you will pull the required images and build your first Docker container.

1. Change directory to first-container/.
* cd first-container/
  
2. Inspect the Dockerfile, and build a container image.
* docker build -t first-container .

3. view the Docker images.
* docker image ls
* The application being served sits on port 8080 in the container image.

4. Publish port 8080 to your AWS Cloud9 host and make it available on port 8080.
* docker run -d -p 8080:8080 --name webapp first-container

5. View the running Docker containers.
* docker ps

6. View the logs that are being captured from the container.
* docker logs webapp
* You will now view the application in a browser.

7. At the top of your AWS Cloud9 instance, choose Preview and then choose Preview Running Application.
* You should see the running application.

8. Launch a shell inside the container.
* You can use this shell to run commands within the container itself.
* docker exec -it webapp /bin/sh

9. In the container, look at the contents of the /app folder and view the contents of /app/input.txt.
* ls /app
* cat /app/input.txt

10. In the container, view the process list.
* ps -a

11. Escape out of the container (you can escape out of the container by pressing Ctrl+D).
    
12. Stop and remove the running container.
* docker stop webapp
* docker rm webapp

### Task 4: Modifying the container with new data
* In this task, you will change the input.txt file inside the container with new data. You can use a bind mount to mount a local file resource in place of /app/input.txt inside the container.

1. Create an ~/input.txt file with five words, with each word on a new line.
* printf "cinco\ncuatro\ntres\ndos\nuno" > ~/input.txt

2. Launch a container with the new file mounted in place of /app/input.txt.
* docker run -d -p 8080:8080 \
* -e MESSAGE_COLOR=#0000ff \
* -v ~/input.txt:/app/input.txt \
* --name webapp \
* first-container
* You can configure an application that’s running in a container with environment variables. The containerized application takes MESSAGE_COLOR as an environment variable.

3. Visit the updated application in a browser by choosing Preview, Preview Running Application.

4. Force-remove the container.
* docker rm -f webapp


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
