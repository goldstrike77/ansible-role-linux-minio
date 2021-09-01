![](https://img.shields.io/badge/Ansible-minio-green.svg?logo=angular&style=for-the-badge)

>__Please note that the original design goal of this role was more concerned with the initial installation and bootstrapping environment, which currently does not involve performing continuous maintenance, and therefore are only suitable for testing and development purposes,  should not be used in production environments. The author does not guarantee the accuracy, completeness, reliability, and availability of the role content. Under no circumstances will the author be held responsible or liable in any way for any claims, damages, losses, expenses, costs or liabilities whatsoever, including, without limitation, any direct or indirect damages for loss of profits, business interruption or loss of information.__

>__请注意，此角色的最初设计目标更关注初始安装和引导环境，目前不涉及执行连续维护，因此仅适用于测试和开发目的，不应在生产环境中使用。作者不对角色内容之准确性、完整性、可靠性、可用性做保证。在任何情况下，作者均不对任何索赔，损害，损失，费用，成本或负债承担任何责任，包括但不限于因利润损失，业务中断或信息丢失而造成的任何直接或间接损害。__
___

<p><img src="https://raw.githubusercontent.com/goldstrike77/goldstrike77.github.io/master/img/logo/logo_minio.png" align="right" /></p>

__Table of Contents__

- [Overview](#overview)
- [Requirements](#requirements)
  * [Operating systems](#operating-systems)
  * [Minio Versions](#Minio-versions)
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
- [Donations](#Donations)

## Overview
MinIO is a cloud storage server compatible with Amazon S3. As an object store, MinIO can store unstructured data such as photos, videos, log files, backups and container images.

## Requirements
### Operating systems
This Ansible role installs Minio on Linux operating system, including establishing a filesystem structure and server configuration with some common operational features, Will works on the following operating systems:

  * CentOS 7

### Minio versions

The following list of supported the Minio releases:

* All Release

## Role variables
### Main parameters #
There are some variables in defaults/main.yml which can (Or needs to) be overridden:

##### General parameters
* `minio_cluster`: The Minio distributed cluster name, Must sets in hostvars.
* `minio_path`: Specify the Minio data directory.
* `minio_force_https`: A boolean to determine whether or not to Encrypting HTTP client communications.
* `minio_drives`: Defines the number of drives per node.
* `minio_tenants`: Specify the name of tenants.

##### Role dependencies
* `minio_ngx_dept`: A boolean value, whether proxy web interface and API traffic using NGinx.

##### Listen port
* `minio_api_start_port`: The start port of Minio instance API.
* `minio_console_start_port`: The start port of Minio instance Console.

##### NGinx parameters
* `minio_ngx_port_http`: NGinx HTTP listen port.
* `minio_ngx_port_https`: NGinx HTTPs listen port.
* `minio_ngx_client_max_body_size`: The maximum allowed size of the client request body.

##### Server System Variables
* `minio_arg.cache`: Whether enable disk caching feature.
* `minio_arg.cache_expiry`: List of cache exclusion patterns.
* `minio_arg.cache_exclude`: Cache expiry duration in days.
* `minio_arg.cache_quota`: Maximum permitted usage of the cache in percentage.
* `minio_arg.compress_enabled`: Allows streaming compression to ensure efficient disk space usage.
* `minio_arg.compress_extensions`: Which extensions are included by default for compression.
* `minio_arg.compress_mime_types`: Which mime-types are included by default for compression.
* `minio_arg.drive_sync`: Enable synchronous mode for all data operations.
* `minio_arg.uid`: System user ID for running minio services.
* `minio_arg.ulimit_nofile`: The number of files launched by systemd.
* `minio_arg.ulimit_nproc`: The number of processes launched by systemd.
* `minio_arg.user`:  System user name for running minio services.
* `minio_arg.webui`: Enable or Disable access to web UI.

##### Bucket Notification Variables
* `minio_events_arg`: Define the targets for bucket events can be published to.

##### Service Mesh
* `environments`: Define the service environment.
* `datacenter`: Define the DataCenter.
* `domain`: Define the Domain.
* `customer`: Define the customer name.
* `tags`: Define the service custom label.
* `exporter_is_install`: Whether to install prometheus exporter.
* `consul_public_register`: Whether register a exporter service with public consul client.
* `consul_public_exporter_token`: Public Consul client ACL token.
* `consul_public_http_prot`: The consul Hypertext Transfer Protocol.
* `consul_public_clients`: List of public consul clients.
* `consul_public_http_port`: The consul HTTP API port.

### Other parameters

## Dependencies
- Ansible versions >= 2.8
- Python >= 2.7.5
- [NGinx](https://github.com/goldstrike77/ansible-role-linux-nginx.git)

## Example

### Hosts inventory file
See tests/inventory for an example.

    node01 ansible_host='192.168.1.10' minio_cluster='demo'
    node02 ansible_host='192.168.1.11' minio_cluster='demo'
    node03 ansible_host='192.168.1.12' minio_cluster='demo'
    node04 ansible_host='192.168.1.13' minio_cluster='demo'

### Vars in role configuration
Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- hosts: all
  roles:
     - role: ansible-role-linux-minio
       minio_cluster: demo
```

### Combination of group vars and playbook
You can also use the group_vars or the host_vars files for setting the variables needed for this role. File you should change: group_vars/all or host_vars/`group_name`.

```yaml
minio_path: '/data'
minio_force_https: true
minio_drives: 1
minio_tenants:
  - 'others'
  - 'thanos'
minio_ngx_dept: false
minio_api_start_port: '9000'
minio_console_start_port: '9010'
minio_ngx_port_http: '80'
minio_ngx_port_https: '443'
minio_ngx_client_max_body_size: '100m'
minio_arg:
  cache: false
  cache_expiry: '90'
  cache_exclude: "*.pdf"
  cache_quota: '20'
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
minio_events_arg:
  type: 'elasticsearch' 
  url: 'https://demo-prd-infra-monitor-elasticsearch.service.dc01.local:9200'
  index: 'minio-event'
  format: 'access'
  queue_limit: '100000'
  username: 'elastic'
  password: 'changeme'
environments: 'prd'
datacenter: 'dc01'
domain: 'local'
customer: 'demo'
tags:
  subscription: 'default'
  owner: 'nobody'
  department: 'Infrastructure'
  organization: 'The Company'
  region: 'China'
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

## Donations
Please donate to the following monero address.

    46CHVMbb6wQV2PJYEbahb353SYGqXhcdFQVEWdCnHb6JaR5125h3kNQ6bcqLye5G7UF7qz6xL9qHLDSAY3baagfmLZABz75
