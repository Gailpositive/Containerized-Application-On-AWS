# DOCKER-CONTAINERIZATION-ON-AWS
# CONTAINER-Basics

## PART ONE: CREATING-CONTAINER-IN-AWS
###  AWS Technologies Used: 
* AWS Identity and Access Management (IAM) policy and user 
* AWS Cloud9 integrated development environment (IDE) instance
* AWS CloudFormation stack
* Amazon DynamoDB table
  
## PART 2: Create A Private Container Registry Within AWS Elastic Container Registry (ECR) and Deploy It On AWS App Runner
### AWS Technologis Used:
* AWS Cloud9 IDE
*  AWS Identity and Access Management (IAM) policy and user 
* AWS App Runner service
* Amazon Elastic Container Registry (Amazon ECR) repository

### PREREQUISITES: Download a cloudformation template to establish the required backend resources for completing the exercise and config a source code for launching container instances within the AWS Cloud9 environment.

## STEP 1: 
* Open Cloudformation in the AWS management console and create stack 
<img width="957" alt="1" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/be6422a1-956b-4af9-8859-6631966fe51d">

* I already have my template downloade so I Chose template is ready 
<img width="955" alt="2" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/7f6b4391-b254-43e1-bfa0-708f89a14ac4">

* Upload template file
* Choose file and click next
<img width="958" alt="3a" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6a3facaa-dcc0-4319-a1cd-583c03d61f89">

* Open the yaml file from my computer download
<img width="929" alt="4" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/309cc7cf-6a6a-47d5-96de-2ae93b8374be">

* Give the stack same name with the downloaded yaml file
<img width="932" alt="5 stack created and named" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/7423b9ed-49bb-4d50-a859-5ea6500e404a">

* Didnt give it a tag
<img width="949" alt="6   click next" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/4e100968-4450-4bac-a0ff-95c355233515">

* Review template
<img width="944" alt="7 review" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/c06f8be4-445b-48b6-bcd5-f7fb619cb7cf">

* Acknowledge and submit ready template
<img width="946" alt="8 scroll down and acknowledge cloudformation and click next" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/42cdf4c4-8deb-4847-b967-472269d94aa5">

* Stack processing to finish
<img width="928" alt="9 stack in process" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/abbf6722-2326-441b-b63b-2155d8443dc3">


### Task 1: Creating an AWS Cloud9 instance
* Switch over to AWS cloud9
* Create Environment
* Give the environment a name
* Cloud9 IDE to run on  a new EC2 instance
<img width="946" alt="10 create cloud9" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6f047241-478b-4291-a1b9-7803e10e648f">

* On the networkin setting, no external traffic is allow access, Choose AWS system manager
* Config VPC  settings and Attach internet gateway 
<img width="960" alt="11 scroll down to setting choose vpc containers vpc" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/5dac7eee-893e-4a09-8151-03af7acaccd2">


* Successfully created
<img width="921" alt="12 container-cloud9 successfully created" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/e16a328f-27b2-4130-85c9-d0f264e9f893">

## Task 2: Modifying and deploying source code to AWS Cloud9
### In thsi task, I will update the CLI version, deploy source code, associate the instance profile with the cloud9 instance and finally expand the environment to give it more disk space

* In the AWS Cloud9 terminal, I upgrade the AWS CLI version
* Deploy the source code that’s needed to complete the exercise
* Associate the instance profile with my AWS Cloud9 instance
* Finally, I will expand my environment to give it more disk space.
<img width="910" alt="13aws install updated" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/380d38af-e9af-48c0-8939-3a1fdaf39424">

* verify the version
<img width="563" alt="14 very aws version" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/78945a63-b66f-44c9-9cfc-0fc582c517a5">

* Download and extract the source code
<img width="927" alt="15 download and etract source code i need" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/4b6b1e30-be30-441a-be33-b97250dbaa66">

* Replace the current association with the cloud9-containers-role
<img width="749" alt="16 replacing aws association" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/bd495d0e-d7d5-491d-8edf-a943005db051">

* State is listed as associated.
<img width="655" alt="17 state is associated" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/285a90f6-8c8a-44c9-9d8d-3a89e1677a9b">

* Disable credential rotation and utilize cloudformation to created for enhanced control
* Retrieve info about AWS IAM
<img width="694" alt="18 aws get caller identity" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/1bfc7feb-cfd3-4520-b2ef-8e1dfb242f0a">

* Expand the AWS Cloud9 disk by running the following utility
<img width="705" alt="19 bash utilities c9-resize sh 40" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/76f83035-3539-4393-921e-4bcd4084a710">

### Task 3: Building the first container
### In this task, I will pull the required images and build my Docker container.

* Cd to first-container
* build a container image name first-container with the -t flag
<img width="835" alt="20b" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/89bea26d-c289-461b-b60b-b71451afe7dc">

* docker ls to view container created
<img width="748" alt="21 docker image created" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/835cf819-3b0f-4f80-9e17-2511fafbdc03">

* docker run the container detach on port 8080
* docker ps view running docker containers
* Publish port 8080 to the Cloud9 host and make it available on port 8080.
<img width="753" alt="22 docker run d port 8080" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/b2693b10-e631-4f05-943b-5a413e9f9a71">

* View the application in a browser.
* At the top of my AWS Cloud9 instance, Preview and then choose Preview Running Application.
* View the running application.
<img width="941" alt="23 application running on browser" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/0a709db0-f459-43f5-ab81-35a08be717c0">

* Launch a shell inside the container
* docker exec -it webapp /bin/sh
* view process list
* In the container, view the contents of the /app folder and the contents of /app/input.txt.
* Escape out of the container
<img width="768" alt="24 docker exec" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/c149fa9c-b76d-4b70-b6ff-58eab93d86c0">

* Stop and remove the running container.
<img width="764" alt="25 stop and rm running webapp" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/eddb7aa1-77e3-4a29-90b5-947024192942">


### Task 4: Modifying the container with new data
* In this task, I will change the input.txt file inside the container with new data. I can use a bind mount to mount a local file resource in place of /app/input.txt inside the container.

* Create an ~/input.txt file with five words, with each word on a new line and 
* Launch a container with the new file mounted in place of /app/input.txt.
* Configure an application that’s running in a container with environment variables. The containerized application takes MESSAGE_COLOR as an environment variable.
<img width="737" alt="26  create app input text and launch a container with the new file mounted" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/79534299-ffcb-4f87-aac4-099b6dbb7956">


* Visit the updated application in cloud9 browser by choosing Preview, Preview Running Application.
<img width="563" alt="27  view updated application running on broswer" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/054394d6-1bef-43d1-b384-a82dcf23a5c2">

* Force-remove the container.
<img width="756" alt="28 Force remove the container" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/9542365a-ed6b-40c3-b5f0-ab3e2a61a4bf">


<img width="421" alt="29 ECR image" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/b2a1824d-9206-40ab-b816-2805caf62523">

## PART 2: Create A Private Container Registry Within AWS Elastic Container Registry (ECR) and Deploy It On AWS App Runner
### AWS Technologis Used:
* AWS Cloud9 IDE
* AWS Identity and Access Management (IAM) policy and user 
* AWS App Runner service
* Amazon Elastic Container Registry (Amazon ECR) repository

### TASK 1
* In this exercise, I create an Amazon ECR repository,
* Authenticate to Amazon ECR,
* Push my image to the Amazon ECR repository
* Set up and deploy an AWS App Runner service.

* Create ECR repository
* Enter the name and save
<img width="751" alt="30 cretae ECR repo and save" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/c06590c3-9ffd-4784-bd34-b3e1448241e6">

*  Choose the first-container repository link 
<img width="943" alt="31 private repo created" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/fd2cbf51-bda1-43dc-a956-eb5fc7d2bf92">

* click View push commands 
<img width="922" alt="32 click on veiw push cpmmand to view  the commands that you will use from your AWS Cloud9 instance" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/ddbb8011-ce58-443d-bd47-77aad82bc824">

* To see the commands that will be use from your AWS Cloud9 instance to authenticate ECR.
<img width="951" alt="33 view push commands on windows" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/9f066233-aae9-4c9d-852d-862c2db98ac9">

 ### Task 2: Authenticate to Amazon ECR
* In this task, I will authenticate to ECR through the AWS Cloud9 IDE instance by running the push commands (which you saw in ECR).

* Open cloud9 instance
<img width="948" alt="34 Open cloud9 IDE" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/a3a2dfae-d0d8-4847-b669-783dd823b2a1">

* Cd in the first-container
<img width="925" alt="35bcd in first container containing  my docker file" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/3f727e2a-5404-4c09-8b38-4724da588240">

* Build my docker image adding  a new tag flag
<img width="779" alt="36 docker build" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/a0884dd3-b5e2-4b40-b86f-8030ece91bf2">

* filter to view only this particular  docker image 
<img width="725" alt="37 filter reference" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/a115bc0b-8574-4cb5-ac57-ce7f731f2861">

* Retrieve AWS ID
* Retrieve instance metadata
<img width="748" alt="38 account and region" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/2a945462-0393-401a-8d8b-955bce429ca0">

*  Authenticate to ECR registry that my IAM principal has access to
*  Login successful
<img width="767" alt="41 and 42 updated" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/dbe1b44f-4a93-4ebd-beb5-a2de70d0c076">

* Push docker image 
<img width="959" alt="42 b" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/94f48577-b870-4768-8ed7-7509a9122a7e">

### Task 3: Setting up AWS App Runner

* Create app runner 
<img width="951" alt="43 create APP runner" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/4517c6ce-bb2c-4c3a-9d74-f0d026123a91">

* In source and depolyment repository type, choose container 
* Provider is private ECR
* Container image URI, choose Browse.
<img width="946" alt="48" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/29a30dc2-c0d9-4fd3-a2a6-7ce330f3cd97">

<img width="928" alt="46" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/29b40d54-e14a-4f89-8e47-9b639485787c">
<img width="922" alt="47" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/13aa8454-3f17-4da8-8125-feb9037b8591">






<img width="611" alt="39 powershell aws config" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/e580d08a-bd63-4c1b-b043-db76b162d0a5">
