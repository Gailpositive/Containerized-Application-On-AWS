## Docker-Containerization-Introduction

## Notes:Understanding -Docker
### Docker is a container engine
<img width="510" alt="image 1" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6b730a64-603c-446b-9784-74ced0eb59d9">

### What is Virtualization?
* Virtualization is technology or software called hypervisor ,it is use to create virtual representations of servers, storage, networks, and other physical machines
### What is a hypervisor? 
* A hypervisor is a software that is use to run multiple virtual machines on a single physical machine. Example: EC2, Zen, VM ware, Oracle virtual box.. are hypervisor's
* Virtualization aims to run multiple OS instances on a single server...like ec2

### What is containerizatio?
* Containerization is a software (eg Docker engine) deployment process that bundles or packages  an application's code with all the files and libraries it needs to run on any infrastructure.
* It is a lightweight engine
<img width="588" alt="image 2b" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/a3af2d87-6e8e-44ec-b0dd-6e02ac1b2720">

### How to a docker image?
* The developer bundles the Application code, Dependencies, Libraries, Binaries, Directory structures etc in a file called docker file, and ship to docker hub or github,
* The operations personel downloads the docker file to create docker image and creates a docker container.
* A docker container is a runing instance of a docker image.
* You can create as many containers of same image
<img width="621" alt="image3" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/49e05d13-e801-48eb-9a1d-34388e0346c8">



### Installing Docker
* Launch an ec2
* Connect to AWS cloudshell terminall
* Run "which docker" command to check if docker is installed
* sudo apt update -y
* sudo apt install docker.io to install lastest version of docker

 <img width="912" alt="0ne docker not yet installed" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/b69e454a-6ee9-454d-9263-db55280581c8">
<img width="905" alt="two install docker lastest version after update -y" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/eab73a21-a79e-4627-b96f-fdee2d7de01e">
<img width="817" alt="three" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/7e8c6f1f-fe8a-467a-b30e-4feb8cbcfcc7">
 
### Docker Architecture
<img width="536" alt="image 3 docker architecture" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/22262b66-b42f-473a-9046-24cd10298947">
<img width="927" alt="four" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/52d77bbf-87d2-4e40-8d4b-766236086dad">
* There is a docket client and docker server 
* Every commands i run, is from the client, interacting with the docker deamon /docker engine
