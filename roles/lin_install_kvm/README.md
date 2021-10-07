NAME: lin_install_kvm
=========================

Summary: This role is designed to install kvm for lab testing. 

### Requirements

System CPU must support virtualization

### Tasks

| Task Number |      Tasks Play       |                             Description                             |
| :---------- | :-------------------- | :------------------------------------------------------------------ |
| 1           | gate.yml              |                                                                     |
| 1.1         |                       |                                                                     |
| 2           | main.yml              | Main play to call other plays in the role                           |
| 3           | centos.yml            | Play to install KVM on CentOS                                       |
| 3.1         | builtin.package       | Install all the packages required to run KVM                        |
| 3.2         | builtin.service       | Start and enbale all services required to run KVM                   |
| 3.3         | builtin.service_facts | Collect the service facts to output services that should be running |
| 3.4         | builtin.debug         | output services that should be started and running                  |
| 4           | rocky.yml             | Play to install KVM on Rocky                                        |
| 5           | ubuntu.yml            | Play to install KVM on Ubuntu                                       |

### Global Variables

| Variable | Default Value | Description | Required |
| :------- | :------------ | :---------- | :------- |
|          |               |             |          |


### Role Variables

|   Variable   | Default Value |                    Description                     | Required |
| :----------- | :------------ | :------------------------------------------------- | :------- |
| rhel_based   | list          | List of packages for a RHEL based install of KVM   | Yes      |
| ubuntu_based | list          | List of packages for a Ubuntu based install of KVM | Yes      |
| user_pass    | hashed string | Password for kvm_admin                             | yes      |

### Extra Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Registered Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Ansible Facts

| Fact | Description |
|:-----|:------------|
|      |             |

### Dependencies

* None

### Example Playbook

### Ansible Base Command Line

### Ansible AWX

### Morpheus 

### License

N/A

### Author Information

|         |                 |
| :------ | :-------------- |
| Contact | Todd A. Kearney |
| Email   | mailto://       |
| Version | 0.0.1           |