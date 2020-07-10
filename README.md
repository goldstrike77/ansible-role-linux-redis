![](https://img.shields.io/badge/Ansible-redis-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_redis.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Redis Versions](#redis-versions)
- [ Role variables](#Role-variables)
  * [Main Configuration](#Main-parameters)
  * [Other Configuration](#Other-parameters)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Hosts inventory file](#Hosts-inventory-file)
  * [Vars in role configuration](#vars-in-role-configuration)
  * [Combination of group vars and playbook](#combination-of-group-vars-and-playbook)
- [License](#license)
- [Author Information](#author-information)
- [Contributors](#Contributors)

## Overview
Redis provides high availability via Redis Sentinel distributed system. Sentinel helps to monitor Redis instances, detect failures and will do roles switches automatically thus enabling a Redis deployment to resist any kind of failures.

It features monitoring of Redis instances (master and replicas), supports notification of other services/processes or the system administrator, automatic failover to promote a replica to a master when the master goes down and provides configuration for clients to discover the current master offering a particular service.

## Requirements
### Operating systems
This Ansible role installs Redis on linux operating system, including establishing a filesystem structure and server configuration with some common operational features, Will works on the following operating systems:

  * CentOS 7

### Redis versions

The following list of supported the Redis releases:

* Redis 5, 6

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:
##### General parameters
* `redis_version`: Specify the Redis version.
* `redis_path`: Specify the Redis data directory.
* `redis_authorization`: A boolean value, Enable or Disable authentication.
* `redis_requirepass`: Authorization clients password.
* `redis_ssl`: A boolean value, whether Encrypting client and cluster communications.
* `redis_cluster_name`: Cluster name of servers that implements distribution performance.
* `redis_cluster_mode`: Defines type of cluster type: sentinel / standalone.

##### Listen port
* `redis_port`: Redis listen.
* `redis_exporter_port`: Prometheus Redis exporter.
* `redis_sentinel_port`: Redis sentinel listen.
* `redis_sentinel_exporter_port`: Prometheus Redis Sentinel exporter.

##### Backup parameters
* `redis_backupset_arg.keep`: Backup retention cycle in days.
* `redis_backupset_arg.encryptkey`: BackupSet encryption key.
* `redis_backupset_arg.cloud_rsync`: Whether rsync for cloud storage.
* `redis_backupset_arg.cloud_drive`: Specify the cloud storage providers.
* `redis_backupset_arg.cloud_bwlimit`: Controls the bandwidth limit.
* `redis_backupset_arg.cloud_event`: Define transfer events.
* `redis_backupset_arg.cloud_config`: Specify the cloud storage configuration.

##### Server System Variables
* `redis_tcp_backlog`: TCP listen backlog.
* `redis_timeout`: Client connection idle time in seconds.
* `redis_tcp_keepalive`: Client keepalive time in seconds.
* `redis_maxclients`: The max number of connected clients at the same time.
* `redis_maxmemory`: A memory usage limit to the specified amount in MB.
* `redis_ulimit_nproc`: The number of processes launched by systemd.
* `redis_ulimit_nofile`: The number of files launched by systemd.
* `redis_renamed_commands`: Disabling of specific commands.

##### Service Mesh
* `environments`: Define the service environment.
* `datacenter`: Define the DataCenter.
* `domain`: Define the Domain.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_http_prot`: The consul Hypertext Transfer Protocol.
* `consul_public_http_port`: The consul HTTP API port.
* `consul_public_clients`: List of public consul clients.

### Other parameters
There are some variables in vars/main.yml:

* `redis_kernel_parameters`: Operating system variables.

## Dependencies
- Ansible versions >= 2.8
- Python >= 2.7.5

## Example
### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  roles:
     - role: ansible-role-linux-redis
```

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`.

```yaml
redis_version: '5'
redis_path: '/data'
redis_authorization: true
redis_requirepass: 'changme'
redis_ssl: false
redis_cluster_name: 'cluster01'
redis_cluster_mode: 'standalone'
redis_port: '6379'
redis_exporter_port: '9121'
redis_sentinel_port: '26379'
redis_sentinel_exporter_port: '9355'
redis_backupset_arg:
  keep: '7'
  encryptkey: 'HgDEvnj5bfcq'
  cloud_rsync: false
  cloud_drive: 'azureblob'
  cloud_bwlimit: '10M'
  cloud_event: 'sync'
  cloud_config:
    account: 'blobuser'
    key: 'base64encodedkey=='
    endpoint: 'blob.core.chinacloudapi.cn'
redis_tcp_backlog: '16384'
redis_timeout: '300'
redis_tcp_keepalive: '60'
redis_maxclients: '10000'
redis_maxmemory: '1024'
redis_ulimit_nproc: '65535'
redis_ulimit_nofile: '65535'
redis_renamed_commands:
  - 'CONFIG'
  - 'DEBUG'
  - 'SHUTDOWN'
environments: 'Development'
datacenter: 'dc01'
domain: 'local'
tags:
  subscription: 'default'
  owner: 'nobody'
  department: 'Infrastructure'
  organization: 'The Company'
  region: 'China'
exporter_is_install: false
consul_public_register: false
consul_public_exporter_token: '00000000-0000-0000-0000-000000000000'
consul_public_http_prot: 'https'
consul_public_http_port: '8500'
consul_public_clients:
  - '127.0.0.1'
```

## License
![](https://img.shields.io/badge/MIT-purple.svg?style=for-the-badge)

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.
