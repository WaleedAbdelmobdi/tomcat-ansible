## Role info

> Ansible Role to Install Tomcat 9 on CentOS.


## Tested on the following operating systems

- CentOS 8

## Tasks in the role

This role contains tasks to:

- Install basic packages required
- Install Java
- Add tomcat user and group
- Download tomcat and install - configure systemd
- Configure firewall
- Change default Port
- Deploy index.html file

## Usage

- Clone the Project:

```
$ git clone https://github.com/WaleedAbdelmobdi/tomcat-ansible.git
$ cd tomcat-ansible
```

- Update hosts file

```
$ vim hosts
[tomcat-nodes]
192.168.10.10       # Remote user to act on
```

- Update variables in playbook file - Set Tomcat version, remote user and Tomcat UI access credentials

```
$ vim tomcat-setup.yml
- name: Tomcat deployment playbook
  hosts: tomcat-nodes       # Inventory hosts group / server to act on
  become: yes               # If to escalate privilege
  become_method: sudo       # Set become method
  remote_user: root         # Update username for remote server
  vars:
    tomcat_ver: 9.0.30                          # Tomcat version to install
    ui_manager_user: manager                    # User who can access the UI manager section only
    ui_manager_pass: Str0ngManagerP@ssw3rd      # UI manager user password
    ui_admin_username: admin                    # User who can access bpth manager and admin UI sections
    ui_admin_pass: Str0ngAdminP@ssw3rd          # UI admin password
  roles:
    - tomcat
```

If you are using non root remote user, then set username and enable sudo:

```
become: yes
become_method: sudo
```

## Running Playbook

Once all values are updated, you can then run the playbook against your nodes.

Playbook executed as root user - with ssh key:

```
$ ansible-playbook -i hosts tomcat-setup.yml
```

Playbook executed as root user - with password:

```
$ ansible-playbook -i hosts tomcat-setup.yml --ask-pass
```

Playbook executed as sudo user - with password:

```
$ ansible-playbook -i hosts tomcat-setup.yml --ask-pass --ask-become-pass
```

Playbook executed as sudo user - with ssh key and sudo password:

```
$ ansible-playbook -i hosts tomcat-setup.yml --ask-become-pass
```

Playbook executed as sudo user - with ssh key and passwordless sudo:

```
$ ansible-playbook -i hosts tomcat-setup.yml --ask-become-pass
```


- Test the Tomcat Installation 

Open your browser and type: http://<your_domain_or_IP_address>:9095

- Test the Tomcat Installation 

Open your browser and type: http://<your_domain_or_IP_address>:9095/app/