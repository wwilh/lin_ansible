lin_ad_join_computer
=========================

This Role is designed to join a Linux server to an Active Directory Domain and create a group in active directory for the server that just joined the domain.

### Requirements
All required packages to run this role will be installed by the role. The main.yml file should be encrypted as it contains passwords and senstive information for vars. No log has been set so that passwords are not logged to the command line or in log files. 


### Tasks

| Task Number | Tasks Play      | Description                                                                        |
|:------------|:----------------|:-----------------------------------------------------------------------------------|
| 1           | main.yml        | Determin OS and which OS.yml to run.                                               |
| 2.0         | CentOS.yml      | This task list will be run if the OS is determined to be CentOS and is in the Lab  |
| 2.1         |                 | Include lab.yml vars                                                               |
| 2.2         |                 | Install the required packages for CentOS                                           |
| 2.3         |                 | Install pexpect to use in the code                                                 |
| 2.4         |                 | Install the realm configuration files                                              |
| 2.5         |                 | Join the realm                                                                     |
| 2.6         |                 | Create the server group in AD                                                      |
| 2.7         |                 | Print out the results of the join to AD and creation of the groups in AD           |
| 2.8         |                 | Permit group logins                                                                |
| 2.9         |                 | Permit lab admins logins                                                           |
| 2.10        |                 | Disable global cataloging                                                          |
| 2.11        |                 | Turn off using fully qualified names. This task uses a notifier to restart sssd    |
| 2.12        |                 | Add the lab linux sudoers file onto the server                                     |
| 3.0         | RedHat.yml      | This task will be run if the OS is determined to be RedHat and not in the lab      |
| 3.1         |                 | Install the required packages for RedHat                                           |
| 3.2         |                 | Install the realm configuration files                                              |
| 3.3         |                 | Install nsswitch configuration file                                                |
| 3.4         |                 | Join the realm                                                                     |
| 3.5         |                 | Create the server group in AD                                                      |
| 3.6         |                 | Print out the results of the join to AD and creation of the groups in AD           |
| 3.7         |                 | Permit group logins                                                                |
| 3.8         |                 | Disable global cataloging                                                          |
| 3.9         |                 | Turn off using fully qualified names. This task uses a notifier to restart sssd    |
| 4.0         | OracleLinux.yml | This task will be run if the OS is determined to be OracleLinux and not in the lab |
| 4.1         |                 | Install the required packages for RedHat(same for Oracle)                          |
| 4.2         |                 | Install the realm configuration files                                              |
| 4.3         |                 | Install nsswitch configuration file                                                |
| 4.4         |                 | Join the realm                                                                     |
| 4.5         |                 | Create the server group in AD                                                      |
| 4.6         |                 | Print out the results of the join to AD and creation of the groups in AD           |
| 4.7         |                 | Permit group logins                                                                |
| 4.8         |                 | Disable global cataloging                                                          |
| 4.9         |                 | Turn off using fully qualified names. This task uses a notifier to restart sssd    |
| 5.0         | Ubuntu.yml      | This task will be run if the OS is Ubuntu and in the lab                           |
| 5.1         |                 | Include lab.yml vars                                                               |
| 5.2         |                 | Install the required packages for CentOS                                           |
| 5.3         |                 | Install pexpect to use in the code                                                 |
| 5.4         |                 | Install the realm configuration files                                              |
| 5.5         |                 | Join the realm                                                                     |
| 5.6         |                 | Create the server group in AD                                                      |
| 5.7         |                 | Print out the results of the join to AD and creation of the groups in AD           |
| 5.8         |                 | Permit group logins                                                                |
| 5.9         |                 | Permit lab admins logins                                                           |
| 5.10        |                 | Disable global cataloging                                                          |
| 5.11        |                 | Turn off using fully qualified names. This task uses a notifier to restart sssd    |
| 5.12        |                 | Add the lab linux sudoers file onto the server                                     |


### Global Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Role Variables

|      Variable      |  Default Value   |                      Description                       | Required |
| :----------------- | :--------------- | :----------------------------------------------------- | :------- |
| ad_packages_rhel   | List of packages | Packages to install for RHEL and OEL                   | yes      |
| ad_packages_ubuntu | List of Packages | Packages to install for Ubuntu                         | yes      |
| ad_packages_centos | list of packages | Packages for CentOS                                    | yes      |
| realm              |                  | Realm to join                                          | yes      |
| realm_admin        | see vault        | Administrator that can join machine to realm           | yes      |
| group_ou           | see vault        | Group DN to create group for Linux system              | yes      |
| computer_ou        | see vault        | Couputer DN to put computer in                         | yes      |
| realm_password     | see vault        | Password to use for administrator making changes in AD | yes      |
| root_admin_group   | see vault        | Group for the that is the default admin group          | no       |

### Extra Variables

| Variable | Default Value | Description | Required |
|:---------|:--------------|:------------|:---------|
|          |               |             |          |

### Registered Variables

|   Variable    | Default Value |                                                        Description                                                         | Required |
| :------------ | :------------ | :------------------------------------------------------------------------------------------------------------------------- | :------- |
| realm_results |               | Results from connecting to the realm, This can be either 0 or 1 if it the vaule returned is 1 the machine is already in AD |          |
| group_results |               | Results from creating the group. This can be either 0 or 1 if it the vaule returned is 1 the group already exist           |          |

### Ansible Facts

| Fact             | Description               |
|:-----------------|:--------------------------|
| ansible_hostname | Short hostname of machine |

### Dependencies

* This role uses adcli to create the group in Active Directory, this is installed as one of the first steps of the role. 

### Example Playbook
    ---
    - name: Join AD 
      hosts: all
      become: true
      vars_files:
        - ./vars/morpheus_vars.yml
      roles:
        - role: lin_ad_join_computer

### Ansible Base Command Line
    ansible-playbook -i 'inventory,' lin_ad_join_computer.yml -e instance_type_name='prod,dev,Lab' -u userwithroot --ask-vault-pass -bk

### extra-variables - This is for when the default variables dont work for your needs
    ansible-playbook -i 'inventory,' lin_ad_join_computer.yml -e realm="limited.brands.com" -u userwithroot --ask-vault-pass -bk

ansible-playbook -i 'inventory,' --ask-vault-pass lin_ad_join_computer.yml -e instance_type_name='prod,dev,Lab' -u userwithroot -bk  
Note: The instance_type_name="Lab" is for a lab machine
### Ansible AWX
    Linux - Join Server to Active Directory(SSSD) (template)

### Morpheus 
    Linux - Join Server to Active Directory(SSSD) (task)

### License

N/A

### Author Information

|         |                          |
|:--------|:-------------------------|
| Contact | Todd Kearney             |
| Email   |  |
| Version | 2.0.1                    |