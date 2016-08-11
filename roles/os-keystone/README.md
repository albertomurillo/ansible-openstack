os-keystone
=========

Install keystone.

Requirements
------------

* An existing database server

Role Variables
--------------

Have a look at [defaults/main.yml](https://github.com/albertomurillo/ansible-openstack/blob/master/roles/os-keystone/defaults/main.yml)

Dependencies
------------

* [os-common](https://github.com/albertomurillo/ansible-openstack/tree/master/roles/os-common)

Example Playbook
----------------

    - hosts: controller
      roles:
        - os-keystone

License
-------

Apache

Author Information
------------------

This role was created by [Alberto Murillo](mailto:albertomurillosilva@gmail.com)
