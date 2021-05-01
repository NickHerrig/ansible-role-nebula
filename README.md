# ansible-role-nebula

An Ansible Role that installs [Nebula](https://www.defined.net/nebula/)
on Linux.

## Docs

## Requirements
### Lighthouse is Required
An virtual machine with a static public IP address.
This virtual machine is a needed piece of the nebula 
architecture called a
[Lighthouse](https://www.defined.net/nebula/introduction/#components-of-a-nebula-network)

### Nebula binaries Installed on Localhost 
This role currently requires localhost to be the certificate authority.
Because this role creates and distributes certificates, nebula and 
nebula-cert must be installed on the ansible machine. 

## Role Variables

TBD


## Example Playbook

```yaml
  - hosts: all 
    roles:
    - nickherrig.ansible-role-nebula
```

# License

MIT / BSD

# Author Information

This role was created in 2021 by [Nick Herrig](nickherrig.com).
