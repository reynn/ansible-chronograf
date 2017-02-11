Chronograf
========

[![Build Status](https://travis-ci.org/reynn/ansible-chronograf.svg?branch=master)](https://travis-ci.org/reynn/ansible-chronograf)

Installs and configures Chronograf.

Requirements
------------

This role requires Ansible 1.9 or higher.

Role Variables
--------------

| Name                                  | Default                | Description                                                                                  |
|:--------------------------------------|:-----------------------|:---------------------------------------------------------------------------------------------|
| chronograf_version                    | 1.2.0                                         | The version of Chronograf to install
| chronograf_signing_key_url            | https://repos.influxdata.com/chronograf.key            | Url to the InfluxData GPG key
| chronograf_yum_repo_baseurl           | https://repos.influxdata.com/centos/{{ ansible_distribution_major_version }}/{{ ansible_architecture }}/stable           | Base URL for Yum to download from InfluxData
| chronograf_http_bind_address          | :8086            | The IP and Port to bind the service to |
| chronograf_local_db                   | chronograf.db    | Path to local database file to use or create for storing Chronograf application data. |
| chronograf_query_response_bytes_limit | 2500000          | Maximum response size in bytes, for queries that pass through Chronograf. |

Dependencies
------------

None

Example Playbook
----------------

Install Chronograf
```yaml
- hosts: all
  roles:
    - reynn.chronograf
```

License
-------

BSD

Author Information
------------------

Nic Patterson
