# ansible-role-nebula

*This role is currently under development*

An Ansible Role that installs [Nebula](https://www.defined.net/nebula/)
on Linux.

## Docs
Prior to using this role, I'd recommend giving the 
[general nebula](https://www.defined.net/nebula/introduction/) 
documentation a skim.

## Requirements

### A Lighthouse is Required
A nebula lighthouse is an host with a static public IP address.
The purpose of this machines can be read about in the nebula 
[docs](https://www.defined.net/nebula/introduction/#components-of-a-nebula-network)

### Nebula binaries Installed on Localhost 
For simplicity, This role currently requires localhost to be the certificate authority.
Because this role creates and distributes certificates, nebula-cert must 
be installed on the ansible machine. 

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
