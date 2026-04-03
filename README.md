# [Ansible role rundeck](#ansible-role-rundeck)

Install and configure rundeck on your system.

|GitHub|Issues|Pull Requests|Version|Downloads|
|------|------|-------------|-------|---------|
|[![github](https://github.com/buluma/ansible-role-rundeck/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-rundeck/actions/workflows/molecule.yml)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-rundeck.svg)](https://github.com/buluma/ansible-role-rundeck/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-rundeck.svg)](https://github.com/buluma/ansible-role-rundeck/pulls/)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-rundeck.svg)](https://github.com/buluma/ansible-role-rundeck/releases/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/rundeck)](https://galaxy.ansible.com/ui/standalone/roles/buluma/rundeck/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-rundeck/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- become: true
  gather_facts: true
  hosts: all
  name: Converge
  roles:
    - role: buluma.rundeck
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-rundeck/blob/master/molecule/default/prepare.yml):

```yaml
---
- become: true
  gather_facts: false
  hosts: all
  name: Prepare
  roles:
    - role: buluma.bootstrap
    - role: buluma.java
    - role: buluma.common
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-rundeck/blob/master/defaults/main.yml):

```yaml
---
rundeck_address: "{{ ansible_all_ipv4_addresses[0] | default('127.0.0.1') }}"
rundeck_config:
  - parameter: server.address
    value: "{{ rundeck_address }}"
  - parameter: grails.serverURL
    value: "{{ rundeck_url }}"
  - parameter: dataSource.url
    value: jdbc:h2:file:/opt/rundeck/server/data/grailsdb;MVCC=true
rundeck_framework:
  - parameter: framework.server.hostname
    value: "{{ ansible_fqdn }}"
  - parameter: framework.server.name
    value: "{{ ansible_hostname }}"
  - parameter: framework.projects.dir
    value: "{{ rundeck_rdeckbase }}/projects"
  - parameter: framework.var.dir
    value: "{{ rundeck_rdeckbase }}/var"
  - parameter: framework.logs.dir
    value: "{{ rundeck_rdeckbase }}/var/logs"
  - parameter: framework.rundeck.url
    value: "{{ rundeck_url }}"
  - parameter: framework.ssh-connect-timeout
    value: 0
  - parameter: framework.ssh-command-timeout
    value: 0
  - parameter: framework.rundeck.execution.script.tokenexpansion.enabled
    value: true
rundeck_maxmetaspacesize: 128
rundeck_plugins: []
rundeck_port: 4440
rundeck_rdeckbase: /opt/rundeck
rundeck_release_date: 20211221
rundeck_server_web_context: ""
rundeck_users:
  - password: admin
    roles: user,admin
    username: admin
  - password: user
    roles: user
    username: user
rundeck_version: "3.4.9"
rundeck_xms: 256
rundeck_xmx: 4096
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-rundeck/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub |
|-------------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|
|[buluma.common](https://galaxy.ansible.com/buluma/common)|[![Build Status GitHub](https://github.com/buluma/ansible-role-common/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-common/actions)|
|[buluma.core_dependencies](https://galaxy.ansible.com/buluma/core_dependencies)|[![Build Status GitHub](https://github.com/buluma/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-core_dependencies/actions)|
|[buluma.java](https://galaxy.ansible.com/buluma/java)|[![Build Status GitHub](https://github.com/buluma/ansible-role-java/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-java/actions)|
|[buluma.service](https://galaxy.ansible.com/buluma/service)|[![Build Status GitHub](https://github.com/buluma/ansible-role-service/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-service/actions)|

## [Context](#context)

This role is part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-rundeck/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/robertdebock/enterpriselinux)|all|
|[Debian](https://hub.docker.com/r/robertdebock/debian)|all|
|[Fedora](https://hub.docker.com/r/robertdebock/fedora)|all|
|[Ubuntu](https://hub.docker.com/r/robertdebock/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done on:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them on [GitHub](https://github.com/buluma/ansible-role-rundeck/issues).

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-rundeck/blob/master/LICENSE).

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)

