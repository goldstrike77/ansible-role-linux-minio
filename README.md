## Minio
![](https://img.shields.io/badge/Ansible-minio-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_minio.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Minio Versions](#Minio-versions)
- [ Role variables](#Role-variables)
  * [Minimal Configuration](#minimal-configuration)
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
This Ansible role installs  Minio on linux operating system, including establishing a filesystem structure and server configuration with some common operational features.

## Requirements
### Operating systems
This role will work on the following operating systems:

  * CentOS 7

### Minio versions

The following list of supported the Minio releases:

* All Release

## Role variables
### Minimal configuration

In order to get the Minio running, you'll have to define the following properties before executing the role:

* minio_cluster

The `minio_cluster` should contain the Minio distributed cluster name.

### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `minio_cluster`: Specify the distributed cluster name.
* `minio_path`: Specify the Minio data directory.
* `minio_tenants`: Specify the number of tenants.

##### Listen port
* `minio_start_port`: The start port of Minio instance.

##### Server System Variables
* `minio_arg.compress_enabled`: Allows streaming compression to ensure efficient disk space usage.
* `minio_arg.compress_extensions`: Which extensions are included by default for compression.
* `minio_arg.compress_mime_types`: Which mime-types are included by default for compression.
* `minio_arg.drive_sync`: Enable synchronous mode for all data operations.
* `minio_arg.uid`: System user ID for running minio services.
* `minio_arg.ulimit_nofile`: The number of files launched by systemd.
* `minio_arg.ulimit_nproc`: The number of processes launched by systemd.
* `minio_arg.user`:  System user name for running minio services.
* `minio_arg.webui`: Enable or Disable access to web UI.

### Other parameters
There are some variables in vars/main.yml:

## Dependencies
There are no dependencies on other roles.

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' minio_cluster='demo'
    node02 ansible_host='192.168.1.11' minio_cluster='demo'
    node03 ansible_host='192.168.1.12' minio_cluster='demo'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - role: ansible-role-linux-minio
           minio_cluster: demo

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`

    minio_path: '/data'
    minio_tenants: '2'
    minio_start_port: '9000'
    minio_arg:
      compress_enabled: 'true'
      compress_extensions:
        - 'txt'
        - 'log'
        - 'csv'
        - 'json'
      compress_mime_types:
        - 'text/csv'
        - 'text/plain'
        - 'application/json'
      drive_sync: 'on'
      uid: '2021'
      ulimit_nofile: '65535'
      ulimit_nproc: '65535'
      user: 'minio'
      webui: 'on'

## License

MIT

## Author Information
Please send your suggestions to make this role better.

## Contributors
Special thanks to the [Connext Information Technology](http://www.connext.com.cn) for their contributions to this role.