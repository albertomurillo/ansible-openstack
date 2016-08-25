os-glance
=========

Install glance.

Requirements
------------

* An existing database server
* An existing keystone server

Role Variables
--------------

Have a look at [defaults/main.yml](https://github.com/albertomurillo/ansible-openstack/blob/master/roles/os-glance/defaults/main.yml)

Dependencies
------------

* [os-common](https://github.com/albertomurillo/ansible-openstack/tree/master/roles/os-common)

Example Playbook
----------------

    - hosts: controller
      roles:
        - os-glance

License
-------

Apache

Author Information
------------------

This role was created by [Alberto Murillo](mailto:albertomurillosilva@gmail.com)
