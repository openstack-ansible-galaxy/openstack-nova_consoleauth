Nova consoleauth
=========

OpenStack Nova consoleauth service installation

_Tested on Ubuntu Precise (12.04) and Trusty (14.04)_

Requirements
------------

A RabbitMQ server. See below.

For RHEL/CentOS, RHOSP or RDO repositories are needed.

Role Variables
--------------
### Nova consoleauth (set by this role)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `my_ip` | `{{ ansible_eth0.ipv4.address }}` | Management IP for nova-consoleauth ||
| `console_public_hostname` | `localhost` | Publicly visible name for this console host ||
| `console_token_ttl` | `600` | How many seconds before deleting tokens ||
| `consoleauth_manager` | `nova.consoleauth.manager.ConsoleAuthManager` | Manager for console auth ||

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: consoleauth001
      roles:
        - role: openstack-nova_consoleauth
          rabbit_username: "openstack-nova"
          rabbit_pass: "{{ RABBIT_NOVA_PASS }}"

---

A complete Ansible playbook demo, which uses this role, is available on Github (openstack-ansible-galaxy/vagrant-ansible-openstack) <https://github.com/openstack-ansible-galaxy/vagrant-ansible-openstack>

---

Credits
-------
RedHat support implemented by Abel Boldú <abel.boldu@gmx.com>


License
-------

Apache

Author Information
------------------

Davide Guerri - davide.guerri@gmail.com
