Ansible Role Thanos
=========

Deploy various Thanos components with Podman.

Requirements
------------

This requires the containers.podman collection: https://galaxy.ansible.com/containers/podman

Role Variables
--------------

https://github.com/dchats1/ansible-role-thanos/blob/main/defaults/main.yml


Dependencies
------------

No dependencies at this time

Example Playbook
----------------

    - hosts: thanos
      roles:
         - ansible-role-thanos

License
-------

BSD

Author Information
------------------

David Chatterton
david@davidchatterton.com
