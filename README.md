# Ansible Role: Configure Hosts

Configures RHEL/CentOS servers and updates their packages.

## Requirements

SSH trafic must be up and running between ansible control node and the servers.

## Role Variables

For the entire list of variables, see `defaults/main.yml`.

Role's behavior/actions are controlled by these booleans:

```yaml
---
# tasks variables
copy_hosts_file: false # copy hosts file to remote hosts
copy_ssh_key: false # configure public ssh key in remotes
speedup_dnf: false # configure dnf speed-ups
max_parallel_downloads: 3 # configure dnf parallel downloads speed-up
install_packages: false # install packages
update_host: false # preform a system-wide update
clean_subscription: true # clean RHEL subscription after package installs and updates
```

These variables controll configuration contents:

```yaml
# user variables
home_dir: /root
ssh_key_name: id_ed25519.pub
ssh_key: "{{ home_dir }}/.ssh/{{ ssh_key_name }}"

user_name: admin # user name to be created
user_pass: admin # user password
keyboard_layout: fr # change default keyboard layout

# custom aliases to configure on remotes
bashrc_aliases: |
  # general aliases
  alias psg="ps aux | grep -v grep | grep"
  alias ...
  alias ...

# RHEL machine subscriptions
redhat_username: redhat_access_login
redhat_password: redhat_access_pass
subscription_pool: 8a82c58b81d513980181dd125a771945 # Developer subscription

# packages to install
packages:
  - vim
  - wget
  - curl
  - ...
```

> **Note:** `user_name`, `user_pass`, `redhat_username` and `redhat_password` variables should be defined in vault-crypted file(s).

## Dependencies

Only `ansible` is needed to run this role.

## Example Playbook

You can use this role with this basic playbook.

```yaml
---
- name: Configure vm
  hosts: vm_guests
  remote_user: root

  tasks:
    - name: Include role host_configure
      ansible.builtin.include_role:
        name: ansible-role-configure-hosts
      vars:
        copy_ssh_key: true
        speedup_dnf: true
        install_packages: true
        clean_subscription: false
```

## License

BSD
