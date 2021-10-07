lin_install_docker
=========================

This role is designed to install docker on linux machines. 
The docker version that will be install will be the latest version of docker on the website. 

### Requirements
The role requires connection the docker repos. 

### Tasks

| Task Number |   Tasks Play   |                                      Description                                       |
| :---------- | :------------- | :------------------------------------------------------------------------------------- |
| 1           | gate.yml       |                                                                                        |
| 1.1         |                |                                                                                        |
| 2           | main.yml       | Main portion of the role. This will call all other tasks required to complete the role |
| 2.1         | CentOS.yml     | Include the CentOS install                                                             |
| 2.2         | Ubuntu.yml     | Include the Ubuntu install                                                             |
| 3           |                | CentOS.yml Install docker for CentOS                                                   |
| 3.1         | yum_repository | add the docker-ce repo                                                                 |
| 3.2         | package        | install the required packages for docker on CentOS                                     |
| 3.3         | service        | start and enable the docker service                                                    |
| 4           |                | Ubuntu.yml Install docker for Ubuntu                                                   |
| 4.1         | apt_repository | Install the repo for Ubuntu                                                            |
| 4.2         | package        | Install the packages for Ubuntu                                                        |
| 4.3         | service        | Start and enable the server for Ubuntu                                                 |

### Global Variables

|   Variable   | Default Value |                             Description                              | Required |
| :----------- | :------------ | :------------------------------------------------------------------- | :------- |
| isCENTOS7    | false         | This variable will use Ansible facts to determine the OS and version | Y        |
| isCENTOS8    | false         | This variable will use Ansible facts to determine the OS and version | Y        |
| isUBUNTU2004 | false         | This variable will use Ansible facts to determine the OS and version | Y        |
| isUBUNTU1804 | false         | This variable will use Ansible facts to determine the OS and version | Y        |


### Role Variables

|   Variable    | Default Value |              Description               | Required |
| :------------ | :------------ | :------------------------------------- | :------- |
| centos_docker | List          | List of packages to install for CentOS | y        |
| ubuntu_docker | List          | List of packages to install for Ununtu | y        |

### Extra Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Registered Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Ansible Facts

|                Fact                |            Description            |
| :--------------------------------- | :-------------------------------- |
| ansible_distribution_major_version | Casted to isCentos<version>       |
| nsible_distribution                | Casted to all osVersion variables |

### Dependencies

* None

### Example Playbook

### Ansible Base Command Line

### Ansible AWX

### Morpheus 

### License

N/A

### Author Information

|         |           |
|:--------|:----------|
| Contact |           |
| Email   | mailto:// |
| Version |           |