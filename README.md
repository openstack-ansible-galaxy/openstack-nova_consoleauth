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
| `nova_consoleauth_database_url` | `sqlite:////var/lib/nova/nova.sqlite` | Database URI ||
| `nova_consoleauth_my_ip` | `{{ ansible_eth0.ipv4.address }}` | Management IP for nova-consoleauth ||
| `nova_consoleauth_public_hostname` | `localhost` | Publicly visible name for this console host ||
| `nova_consoleauth_token_ttl` | `600` | How many seconds before deleting tokens ||
| `nova_consoleauth_manager` | `nova.consoleauth.manager.ConsoleAuthManager` | Manager for console auth ||

### RabbitMQ (must exist)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `nova_consoleauth_rabbit_userid` | `rabbit_username_default` | RabbitMQ username for console auth ||
| `nova_consoleauth_rabbit_password` | `rabbit_pass_default` | RabbitMQ password for console auth ||
| `nova_consoleauth_rabbit_virtual_host`| `/` | RabbitMQ virtual host for console auth ||
| `nova_consoleauth_rabbit_retry_interval` | `1` | Frequency to retry connecting to RabbitMQ ||
| `nova_consoleauth_rabbit_host` | `localhost` | The RabbitMQ broker address where a single node is used ||
| `nova_consoleauth_rabbit_port` | `5672` | The RabbitMQ broker port where a single node is used ||
| `nova_consoleauth_rabbit_hosts` | `$rabbit_host:$rabbit_port` | RabbitMQ HA cluster host:port pairs ||
| `nova_consoleauth_rabbit_ha_queues` | `False` | Use HA queues in RabbitMQ (x-ha-policy: all) ||

### Memcached

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `nova_consoleauth_memcached_servers` | `None` | A comma delimited string of hostname:port combos where the Memcached service runs ||

Dependencies
------------

None

Example Playbook
----------------

    - hosts: consoleauth001
      roles:
        - role: openstack-nova_consoleauth
          nova_consoleauth_rabbit_userid: "openstack-nova"
          nova_consoleauth_rabbit_password: "{{ RABBIT_NOVA_PASS }}"

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
