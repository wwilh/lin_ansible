# lin_set_custom_facts

Install the k24 custom facts using vars supplied at runtime from morpheus  
or with supplied vars from AWX or the command line.

## Tasks
------------
1. Stat to see if RedHat facts file is on the system
2. Get timestamp
3. Check for old notes on server.
4. Backup old lb.facts
5. Put lb.facts on the server for custom facts in satellite6
6. Put lb.facts notes on the server.
7. Put old facts back on machine
8. Create Ansible facts.d directory if it is not there.
9. Link satellite facts to ansible facts

# Requirements
------------

None

# Variables
--------------
## Global
1. k24_instance_context
2. k24_application
3. k24_contact_email_group
4. k24_description
5. k24_created_by
6. k24_floor_room_zone
7. k24_cloud_code
8. k24_tier

## Role
1. ENV - set in the j2 template
2. k24_building - set in the j2 template
3. k24_room - set in the j2 template

## Ansible facts
1. ansible_hostname

## Registered Facts
1. factsDir
2. old_notes
3. time
4. facts

# Dependencies
------------
None

# Example Playbook
----------------
```
---
- hosts: all
  become: True
  gather_facts: yes
  pre_tasks:
    - name: PLAY | include global_vars.yml
      include_vars: ./vars/global_vars.yml
      
    - name: PLAY | include morpheus_vars.yml
      include_vars: ./vars/morpheus_vars.yml

    - name: Play | Setup custom facts
      include_role:
        name: lin_set_custom_facts
```

## Commandline
Base Command:
ansible-playbook -i '<inventory>,' lin_install_custom_facts.yml -e "{k24_instance_context: "", k24_application: "", k24_contact_email_group: "", k24_description: "Must\ use\ escape\ machine", k24_created_by: "username@lb.com", k24_floor_room_zone: "building-location\ of\ room", k24_cloud_code: "vmware/azure", k24_tier: ""}"

## AWX
Linux - Install Custom Facts


