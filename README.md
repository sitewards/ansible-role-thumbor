# Ansible Thumbor Role

This is the Ansible Thumbor role. It's designed for consumption by playbooks, not for consumption by itself.
It installs the Thumbor image server

## Limitations

- Does not make that server available publicly, but rather only on localhost. Exposing the server should be handled
  by another role.
- While the thumbor configuration file exists, it has not been hugely templated -- only as required by the current
  implementation. Contributions for further extension are welcome.

## Justification

At the time of writing, there did not appear to be a role that used systemd to manage it's init, nor the more common
primitives associated with running the daemon.

## Installation

There are two ways to install this role:

### Ansible Galaxy (recommended)

```bash
$ cd path/to/playbook/root
$ cat >> requirements.yaml <<EOF
- src: "https://github.com/sitewards/ansible-role-thumbor"
  version: "master" # <----- Update this to a stable version
  name: "sitewards.thumbor"
EOF
$ ansible-galaxy install -r requirements.yaml
```

### Git Submodules

```bash
$ cd path/to/playbook/root
$ mkdir roles/
$ git submodule add https://github.com/littlemanco/ansible-role-thumbor roles/sitewards.thumbor
```

## Usage

Include this in another ansible playbook. For sample, consider a generic server playbook:

```yaml
---
# $PLAYBOOK_ROOT/server.yaml
- name: "server"
  hosts: all
  become: true
  become_user: "root"
```

Add the reference for the role:

```yaml
# $PLAYBOOK_ROOT/server.yaml
# ...
become_user: "root"
roles
  - "sitewards.thumbor"
```

This will allow the role to be discovered. That's it!

## Configuration

Configuration is defined in `defaults/main.yml`. It must be configured before use.

## Contact

- Web: https://www.sitewards.com/
