# DOCKER-CONTAINERIZATION ON AWS,
# CONTAINER-Basics

## PART ONE: CREATING A CONTAINER
## PART TWO: AWS IMAGE REGISTRY--Amazon ECR and AWS App Runner

###  AWS Technologies Used: 
* AWS Identity and Access Management (IAM) policy and user 
* AWS Cloud9 integrated development environment (IDE) instance
* AWS CloudFormation stack
* Amazon DynamoDB table

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

* To update the CLI version I ran the following command
* curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
* unzip awscliv2.zip
* sudo ./aws/install
* . ~/.bashrc 
<img width="910" alt="13aws install updated" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/380d38af-e9af-48c0-8939-3a1fdaf39424">

* verify the version
<img width="563" alt="14 very aws version" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/78945a63-b66f-44c9-9cfc-0fc582c517a5">

* Download and extract the source code
<img width="927" alt="15 download and etract source code i need" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/4b6b1e30-be30-441a-be33-b97250dbaa66">

<img width="749" alt="16 replacing aws association" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/bd495d0e-d7d5-491d-8edf-a943005db051">

<img width="655" alt="17 state is associated" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/285a90f6-8c8a-44c9-9d8d-3a89e1677a9b">

<img width="694" alt="18 aws get caller identity" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/1bfc7feb-cfd3-4520-b2ef-8e1dfb242f0a">

<img width="705" alt="19 bash utilities c9-resize sh 40" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/76f83035-3539-4393-921e-4bcd4084a710">

<img width="950" alt="20 inspect docker file and build a container" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/06741ae4-2548-4691-87f7-c20058ddee9a">

<img width="835" alt="20b" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/bca42540-863f-4317-869f-79d8901a27dc">







## PART TWO: AWS IMAGE REGISTRY--Amazon ECR and AWS App Runner

### AWS Techonolgies Used:
* AWS TECHNOLOGIES USED
* AWS Identity and Access Management (IAM) policy and user 
* AWS App Runner service



  

