Role Name
=========

Kodo Cloud is a backup solution for Office 365. This role deploys Kodo Cloud Agent 
which is a data-mover (component which integrates with the cloud and executes backup/restore operations)

Requirements
------------

CentOS/RHEL 8 minimal installation and public key authentication between command host and target machine

Role Variables
--------------

Defaults:
```
kodo_repo: "http://repo.storware.eu/kodo-cloud/current/el{{ ansible_distribution_major_version }}"
```

* `kodo_repo` variable points to Kodo Cloud RPM repository
* `kodo_staging_path` - allows to configure where staging space resides on the agent (if agent is remote, mount manually server's staging over NFS first)


Dependencies
------------

N/A

Example Playbook
----------------

This deploys Kodo server on `server` host (only one server can be deployed)
and multiple agents on `agents` hosts

```
- hosts: server
  roles:
   - xe0nic.ansible_kodo_cloud_server

- hosts: agents
  roles:
   - xe0nic.ansible_kodo_cloud_agent
```

Example hosts inventory (you need to make sure that SSH public key authentication for
ansible user provided in inventory is configured):

```
[all:vars]
ansible_user = root

[server]
192.168.155.233

[agents]
192.168.155.233 agent_name=agent1
```

License
-------

MIT

Author Information
------------------

For more information visit product website: https://storware.eu/products/kodo-for-cloud
Documentation: https://storware.gitbook.io/kodo-for-cloud-office365