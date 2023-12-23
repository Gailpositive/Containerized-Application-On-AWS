## Docker-Containerization-Introduction

## Notes:Understanding -Docker
### Docker is a container engine
<img width="510" alt="image 1" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/6b730a64-603c-446b-9784-74ced0eb59d9">

### What is Virtualization?
* Virtualization is technology or software called hypervisor ,it is use to create virtual representations of servers, storage, networks, and other physical machines
### What is a hypervisor? 
* A hypervisor is a software that is use to run multiple virtual machines on a single physical machine. Example: EC2, Zen, VM ware, Oracle virtual box.. are hypervisor's
* Virtualization aims to run multiple OS instances on a single server...like ec2

### What is containerization?
* Containerization is a software (eg Docker engine) deployment process that bundles or packages  an application's code with all the files and libraries it needs to run on any infrastructure.
* It is a lightweight engine
<img width="588" alt="image 2b" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/a3af2d87-6e8e-44ec-b0dd-6e02ac1b2720">

### How to a docker image?
* The developer bundles the Application code, Dependencies, Libraries, Binaries, Directory structures etc in a file called docker file, and ship to docker hub or github,
* The operations personel downloads the docker file to create docker image and creates a docker container.
* A docker container is a runing instance of a docker images or containers
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
* The client communicate with the docker host.
* Every command I input on my terminal is from the client side
* It then interacts and get feedback from the docker deamon also called docker engine on the host side of the docker architecture
* And retures the feedback on the client terminal..feeback can be images etc
* The Registery side of the docker diagram is like a backup storage

### Best way to run docket is from root
<img width="732" alt="five best way to run docker" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/5145d89b-5756-4a66-a927-c26c38d4308d">
* Im no longer geting permission denied because I am runing from the root 
* Server communicates back info about server like numbers of server running etc
<img width="810" alt="six no permission denied" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/53200151-c1cb-484d-bf9f-f522c334f731">

* When I dont have access to the root command, I can use the "usermod" command
* -a appends G, and ubuntu is added as a user in docker
* The goal is to give user ubuntu permision to run docker info without error
* In other case ,I will have to "exit" and login back, but in this case I 
<img width="732" alt="eight" src="https://github.com/Gailpositive/Containerized-Application-On-AWS/assets/111061512/f718a10f-b2ae-40c5-be3e-d75ab0438daf">
