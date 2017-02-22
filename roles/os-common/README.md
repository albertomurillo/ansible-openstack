os-common
=========

This role do two things:
* Defines common variables for other openstack roles
* Install repositories containing OpenStack Ocata packages

Requirements
------------

None

Role Variables
--------------

Have a look at [defaults/main.yml](https://github.com/albertomurillo/ansible-openstack/blob/master/roles/os-common/defaults/main.yml)

Dependencies
------------

This role is a dependency of:
* [os-keystone](https://github.com/albertomurillo/ansible-openstack/tree/master/roles/os-keystone)
* [os-glance](https://github.com/albertomurillo/ansible-openstack/tree/master/roles/os-glance)
* [os-nova](https://github.com/albertomurillo/ansible-openstack/tree/master/roles/os-nova)
* [os-neutron](https://github.com/albertomurillo/ansible-openstack/tree/master/roles/os-neutron)
* [os-horizon](https://github.com/albertomurillo/ansible-openstack/tree/master/roles/os-horizon)


Example Playbook
----------------

    - hosts: all
      roles:
         - os-common

License
-------

Apache

Author Information
------------------

This role was created by [Alberto Murillo](mailto:albertomurillosilva@gmail.com)
