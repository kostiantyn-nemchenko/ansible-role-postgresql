# Yet another Ansible role for PostgreSQL

[![Build Status](https://travis-ci.org/kostiantyn-nemchenko/ansible-role-postgresql.svg?branch=master)](https://travis-ci.org/kostiantyn-nemchenko/ansible-role-postgresql)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-kostiantyn--nemchenko.postgresql-blue.svg)](https://galaxy.ansible.com/kostiantyn-nemchenko/postgresql)

  An Ansible role which installs and configures [PostgreSQL](https://www.postgresql.org) - the world's most advanced open source database.

## Requirements

- **root access**

  _This role requires root privileges, so tell ansible to use `become: true` in any [convenient way](http://docs.ansible.com/ansible/latest/become.html) for you._

## Role Variables

- `postgresql_version`

  _Version of the PostgreSQL to install._ 
  
  Default: 10

- `postgresql_cluster_name`

  _Cluster name. Useful when running several postgres instances on the same machine._

  Default: main

- `postgresql_apt_key_url`

  _APT repository key._

  Default: https://www.postgresql.org/media/keys/ACCC4CF8.asc

- `postgresql_apt_repo`

  _APT repository source._

  Default: `deb http://apt.postgresql.org/pub/repos/apt/ {{ ansible_distribution_release }}-pgdg main`

- `postgresql_apt_packages`
  
  _List of PostgreSQL-related packages to be installed/removed depending on the state._

  Default:
```
  - { pkg: "postgresql-{{ postgresql_version }}",            state: "present" }
  - { pkg: "postgresql-client-{{ postgresql_version }}",     state: "present" }
  - { pkg: "postgresql-contrib-{{ postgresql_version }}",    state: "present" }
  - { pkg: "postgresql-server-dev-{{ postgresql_version }}", state: "present" }
  - { pkg: "postgresql-doc-{{ postgresql_version }}",        state: "present" }
  - { pkg: "postgresql-{{ postgresql_version }}-dbg",        state: "present" }
```

- `postgresql_home_dir`
 
  _Home directory of postgres OS user. Defines the location of .pgpass file._
  
  Default: /var/lib/postgresql

- `postgresql_config_dir`

  _Location of PostgreSQL configuration files (pg_hba.conf, postgresql.conf, pg_ident.conf etc)._

  Default: `/etc/postgresql/{{ postgresql_version }}/{{ postgresql_cluster_name }}`

- `postgresql_port`

  _TCP port the server listens on._

  Default: 5432

- `postgresql_databases`

  _List of databases to be created/deleted depending on the state._

  Default: []

- `postgresql_users`

  _List of users to be created/deleted depending on the state._

  Default: []

- `postgresql_extensions`

  _List of extensions to be created/deleted depending on the state. Currently, only PostgreSQL core extensions, provided by postgresql-contrib package, are supported._

  Default: []

- `postgresql_pgpass_rules`

  _Defines the content of .pgpass file._

  Default: []

- `postgresql_hba_access`

  _List of rules to control client authentication._

  Default: []

- `postgresql_config_settings`

  _List of PostgreSQL server options (GUCs) to be set depending on the state. For more information, see [**postgresql-setting**](https://github.com/kostiantyn-nemchenko/ansible-module-postgresql-setting)._
  
  Default: []

## Dependencies

  This role requires an extra Ansible module [**postgresql-setting**](https://github.com/kostiantyn-nemchenko/ansible-module-postgresql-setting) for configuring PostgreSQL server settings (GUCs).

## Example Playbook

    - hosts: postgresql-servers
      become: yes
      roles:
        - postgresql
