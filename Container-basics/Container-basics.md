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
