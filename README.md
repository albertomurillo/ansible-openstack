# ansible-openstack
This repository aims to provide a simple installation of OpenStack without being too bloated with features that the new user doesn't even need.

## Prerequisites

### PIP
pip is a tool for installing Python packages, we will use pip since it install the latest packages while the distro pacakges are outdated.

    $ sudo apt-get install python-pip

### Ansible

    $ sudo pip install ansible netaddr

Note: ansible might require some dependencies to be build which requires the following libraries to be present on your system
* python-dev
* libffi-dev
* libssl-dev

### Ansible Galaxy roles
Ansible galaxy provides a vast collection of roles that you can use within your playbooks

We will use the following ansible roles:

    $ sudo ansible-galaxy install ericsysmin.chrony    
    $ sudo ansible-galaxy install geerlingguy.mysql
    $ sudo ansible-galaxy install Stouts.rabbitmq

## How to Run
I have included a vagrant file that installs all prerequisites for you

To start the vagrant vm:

    $ vagrant up [ubuntu|centos]

To login into the vm

    $ vagrant ssh [ubuntu|centos]

To start the playbooks

    # cd /ansible-openstack
    # ansible-playbook -i hosts openstack.yml
