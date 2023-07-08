# host_configure

an Ansible role that configures RHEL-like hosts. Most of the role's steps can be disabled via boolean variables.

**Role features:**

- **Basic configuration:**
  - send host's ssh key
  - set keyboard layout
  - send host's `/etc/hosts` file
  - configure host's command alias in guests
- **Package configuration:**
  - configure dnf
  - configure redhat subscription if provisioned guests are running RHEL
  - install packages defined in the `packages` variable
  - Update host
  - Clean obsolete packages
  - Remove RHEL subscription
