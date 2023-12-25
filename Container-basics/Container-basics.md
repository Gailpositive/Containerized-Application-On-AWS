# Container-Basic


### In this exercise, I'll create an AWS Cloud9 instance and modify some of the environment settings. 
### You also install the prerequisites and source code that are needed to launch new container instances inside your AWS Cloud9 environment.

### I'll create the following resources:
* AWS Identity and Access Management (IAM) policy and user (Policies and users are AWS account features, offered at no additional charge)
* AWS Cloud9 integrated development environment (IDE) instance
* AWS CloudFormation stack
* Amazon DynamoDB table

  ### Setting up
* This exercise requires an IAM role that will be used with the AWS Cloud9 instance. 
* It also requires a DynamoDB table that will be set up and then used in a later exercise.
* The CloudFormation stack will create these resources for me.
* I will also need to choose a Region where AWS App Runner is available, in this caes, us-west-2 (https://docs.aws.amazon.com/general/latest/gr/apprunner.html)
* Download the following CloudFormation template: exercise-containers.yml. This template will set up the backend resources that are needed to complete the exercise.
### Note: If you have an existing Virtual Private Cloud (VPC) and it has a Classless Inter-Domain Routing (CIDR) block of 10.16.0.0/16, you must edit the template to change it.
* Sign in to the AWS Management Console as a user that has administrator permissions.
1. Choose Services, and search for and open CloudFormation.
2. Choose Create stack.
3. For Specify template, choose Upload a template file.(https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/DEV-AWS-MO-ContainersRedux/downloads/exercise-containers.yml)
4. Select Choose file and browse to where you downloaded the exercise-containers template.
5. Select the exercise-containers template and choose Open.
6. Choose Next.
7. For Stack name, enter "exercise-containers"
8. Choose Next, and then choose Next again.
9. Select the acknowledgement and choose submit. Wait for the stack to complete.

### Exercise 1: Creating the First Container
In this exercise, I will create an AWS Cloud9 instance and modify some of the environment settings. I will also install the prerequisites and source code that are needed to launch new container instances inside your AWS Cloud9 environment.

### Task 1: Creating an AWS Cloud9 instance
* In this task, I will create an AWS Cloud9 instance.
1. In the AWS Management Console, choose Services, and then search for and open Cloud9.
2. Choose Create environment.
3. For Name, enter "containers-cloud9" and choose Next step.
4. Configure the following settings.
* Instance type: t3.small (2 GiB RAM + 2 vCPU)
* Network settings: VPC settings: Containers VPC
5. Choose Create.

### Task 2: Modifying and deploying source code to AWS Cloud9
* Task 2: Modifying and deploying source code to AWS Cloud9
* In this task, I will upgrade the AWS Command Line Interface (AWS CLI) version (https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) , and deploy the source code that’s needed to complete the exercise. I will also associate the instance profile with my AWS Cloud9 instance. Finally, I  will expand my environment to give it more disk space.
1. In the AWS Cloud9 terminal, upgrade the AWS CLI version by running the following command.
* curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
* unzip awscliv2.zip
* sudo ./aws/install
* . ~/.bashrc 

2. Verify the version.
* aws --version

3. Download and extract the source code that you need for this exercise.
* wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/DEV-AWS-MO-ContainersRedux/downloads/containers-src.zip
* unzip containers-src.zip

4. Replace the current association with the cloud9-containers-role.
* export ASSOC_ID="`aws ec2 describe-iam-instance-profile-associations | grep AssociationId | cut -f2- -d: | tr -d ',' | xargs`"
* aws ec2 replace-iam-instance-profile-association --iam-instance-profile Name=cloud9-containers-role --association-id $ASSOC_ID

5. Make sure that the State is listed as associated.
* "aws ec2 describe-iam-instance-profile-associations"

6. Run the following command.
* This command tells AWS Cloud9 to specifically disable the managed rotated credentials, and instead use the cloud9-containers-role that CloudFormation created from the template.
* "aws cloud9 update-environment  --environment-id $C9_PID --managed-credentials-action DISABLE"

7. Wait for a couple of minutes, and then run the following command:
* "aws sts get-caller-identity"
* You should see an Amazon Resource Name (ARN) that matches a role in the CloudFormation template:
* "arn:aws:sts::0123456789012:assumed-role/cloud9-containers-role/i-xxxxxxxxxxxxxxxxxx"

8. Expand the AWS Cloud9 disk by running the following utility:
* "bash utilities/c9-resize.sh 40"

### Task 3: Building the first container
* In this task, I will pull the required images and build my  first Docker container.
1. Change directory to first-container/.
* cd first-container/

2. Inspect the Dockerfile, and build a container image.
* docker build -t first-container .

3. View the Docker images.
* docker image ls
* The application being served sits on port 8080 in the container image.

4. Publish port 8080 to your AWS Cloud9 host and make it available on port 8080.
* docker run -d -p 8080:8080 --name webapp first-container

5. View the running Docker containers.
* docker ps

6. View the logs that are being captured from the container.
* "docker logs webapp"

7. You will now view the application in a browser.
* At the top of your AWS Cloud9 instance, choose Preview and then choose Preview Running Application.
* You should see the running application.

8. Launch a shell inside the container.
* You can use this shell to run commands within the container itself.
* "docker exec -it webapp /bin/sh"

9. In the container, look at the contents of the /app folder and view the contents of /app/input.txt.
* ls /app
* cat /app/input.txt

10. In the container, view the process list.
* ps -a

11. Escape out of the container (you can escape out of the container by pressing Ctrl+D).

12. Stop and remove the running container.
* "docker stop webapp"
* "docker rm webapp"

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

* I  can configure an application that’s running in a container with environment variables. The containerized application takes MESSAGE_COLOR as an environment variable.

3. Visit the updated application in a browser by choosing Preview, Preview Running Application.

4. Force-remove the container.
* "docker rm -f webapp"

## What is an image registry?
An image registry is a repository where you can store container images. From this registry, both DevOps tools and people can pull down container images to run, deploy, or expand on. Image registries can be public or private. Public registries are useful for providing images that can be used as base images for software development. For example, if your company provided a database engine, you could host images with the database software preinstalled on it. Your customers could then use these images as base images to expand on, which would make it easier for them to get their software up and running. Private registries are useful in situations where you don’t want to expose container images to the public, which is often the case with proprietary software.

## Docker Hub
Docker Hub is a popular repository for container images. It offers a variety of sources for container images that you can use, including images from container community developers, open-source projects, and software vendors. For more information about Docker Hub, see https://www.docker.com/products/docker-hub/
Docker Hub


## Amazon ECR
Amazon Elastic Container Registry (Amazon ECR) is a private, container image registry. With Amazon ECR, you can create multiple repositories to store and share your container images. To make it easier to deploy your containerized application, Amazon ECR integrates with other AWS services—such as Amazon Elastic Container Service (Amazon ECS), Amazon Elastic Kubernetes Service (Amazon EKS), and AWS Lambda.

## Amazon ECR Public
Amazon ECR also offers a highly available repository for your public images. You can create a repository for your authenticated AWS Identity and Access Management (IAM) identities to push to a public image repository. Thus, an unauthenticated user with or without an AWS account can pull from your public repository. For more information and to see a searchable list of public repositories, see the https://gallery.ecr.aws/
Amazon ECR Public Gallery
.

AWS App Runner
AWS App Runner provides a way to run your containerized application on AWS infrastructure. You only need to supply a container image or application source to App Runner. App Runner creates all the infrastructure needed to host your application, and it also supplies you with an HTTP endpoint. App Runner serves your application with end-to-end encryption. As load increases, it will also scale within parameters that you define.
