# Yet another Ansible role for PostgreSQL

[![Build Status](https://travis-ci.org/kostiantyn-nemchenko/ansible-role-postgresql.svg?branch=master)](https://travis-ci.org/kostiantyn-nemchenko/ansible-role-postgresql)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-kostiantyn--nemchenko.postgresql-blue.svg)](https://galaxy.ansible.com/kostiantyn-nemchenko/postgresql)

An Ansible role which installs and configures [PostgreSQL](https://www.postgresql.org) - the world's most advanced open source database.

## Requirements

- **root access**

  _This role requires root privileges, so tell ansible to use `become: true` in any [convenient way](http://docs.ansible.com/ansible/latest/become.html) for you._

## Role Variables

Coming soon.

## Dependencies

* _This role requires an extra Ansible module [**postgresql-setting**](https://github.com/kostiantyn-nemchenko/ansible-module-postgresql-setting) for configuring PostgreSQL server settings (GUCs)._

## Example Playbook

    - hosts: postgresql-servers
      become: yes
      roles:
        - postgresql
