# ansible-role-nebula

An Ansible Role that installs [Nebula](https://www.defined.net/nebula/)
on Linux.

[![CI](https://github.com/NickHerrig/ansible-role-nebula/actions/workflows/ci.yml/badge.svg)](https://github.com/NickHerrig/ansible-role-nebula/actions/workflows/ci.yml)

## Requirements

### A Lighthouse is Required
A nebula lighthouse is an host with a static public IP address.
Digital Ocean, Linode, and Oracle Cloud are all extreemly inexpensive options! 
The purpose of this machines can be read about in the nebula 
[docs](https://www.defined.net/nebula/introduction/#components-of-a-nebula-network).

### Nebula binaries Installed on Localhost 
For simplicity, this role currently requires localhost to be the certificate authority.
Because this role creates and distributes certificates, nebula-cert must 
be installed on the ansible machine. Along with this, you will need the nebula binary
to run nebula on your laptop, so it's best to install the latest 
[release](https://github.com/slackhq/nebula/releases/tag/v1.3.0).

## Role Variables

### Installation Variables

| Variable | Default | Description |
| -------- | --------| ----------- |
| nebula_config_dir | /etc/nebula | directory where certs and configs will live on hosts |
| nebula_version | 1.3.0 | version of nebula to be install on hosts | 
| nebula_arch | linux-amd64 | chip arcitecture of devices used for installing correct nebula binary | 
| nebula_install_dir | /usr/local/bin | location where nebula binary will be installed on hosts | 

### Certificate Authority and Device Confiuration Variables 

| Variable | Default | Description |
| -------- | --------| ----------- |
| nebula_ca | localhost | determines where certificates will be generated and deployed from | 
| nebula_ca_name | ~ | name of the certificate authority, ex: "Myorg, Inc" | 
| nebula_ca_dir | ~ | location where certs will be created and stored | 
| nebula_device_config_dir | ~ | location where device configs will be created and stored | 

### Nebula Network Variables
| Variable | Default | Description |
| -------- | --------| ----------- |
| nebula_cidr | "/24" | determines size of the nebula [cidr block](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#IPv4_CIDR_blocks) | 
| nebula_lighthouse_port | 4242 | static port nebula lighthouse will run on, other hosts use dynamic ports | 
| nebula_lighthouse_private_ip | ~ | private nebula ip address of the lighthouse node | 
| nebula_lighthouse_public_ip | ~ | public static ip address of the lighthouse node | 

### Nebula Host Variables
| Variable | Default | Description |
| -------- | --------| ----------- |
| nebula_is_lighthouse | false | boolean flag for wether host is a nebula lighthouse node | 
| nebula_hostname | ~ | name of the host for the nebula network ex: "webserver" | 
| nebula_ip | ~ | host ip address for the nebula network ex: 10.100.0.12 |
| nebula_groups | ~ | nebula groups the node belongs to ex: "vm,webserver,digitalocean" |
| nebula_outbound_firewall_rules | [see defaults](/defaults/main.yml#L25) | a list of outbound firewall rules for the host |
| nebula_inbound_firewall_rules  | [see defaults](/defaults/main.yml#L29) | a list of inbound firewall rules for the host | 

### Nebula Client Device Variable 
| Variable | Default | Description |
| -------- | --------| ----------- |
| nebula_client_devices | ~ | a list of client devices (laptops/tables/phones) for the nebula network | 


## Example Hosts File

```yaml
---
nebula:
  hosts:
    150.136.6.63:
      nebula_is_lighthouse: true
      nebula_hostname: lighthouse
      nebula_ip: 10.100.14.1
      nebula_groups: "lighthouse,vm"
    150.136.53.59:
      nebula_hostname: webserver
      nebula_ip: 10.100.14.2
      nebula_groups: "webserver,vm"
```

## Example Group Variables

```yaml
---
nebula_ca_name: "Nicks Homelab"
nebula_ca_dir: "~/Desktop/nebula/certs"
nebula_device_config_dir: "~/Desktop/nebula/configs"

nebula_lighthouse_public_ip: 150.136.6.63
nebula_lighthouse_private_ip: 10.100.14.1

nebula_client_devices:
  - nebula_hostname: "laptop"
    nebula_ip: 10.100.14.20
    nebula_groups: "laptop,ssh"
    nebula_outbound_firewall_rules: |
      - port: any
        proto: any
        host: any
    nebula_inbound_firewall_rules: |
      - port: any
        proto: icmp
        host: any
  - nebula_hostname: "phone"
    nebula_ip: 10.100.14.21
    nebula_groups: "phone"
    nebula_outbound_firewall_rules: |
      - port: any
        proto: any
        host: any
    nebula_inbound_firewall_rules: |
      - port: any
        proto: icmp
        host: any
```

## Example Playbook

```yaml
  - hosts: all 
    roles:
    - nickherrig.nebula
```

## Docs
Prior to using this role, I'd recommend giving the 
[general nebula](https://www.defined.net/nebula/introduction/) 
documentation a skim.

## Contributing
This role is heavily influenced from the setup steps documented 
in the nebula [quick start](https://www.defined.net/nebula/quick-start/)
documentation. It tries to balance simplicity with custimization options.
Because of this it doesn't contain some of the highly custamizable nebula 
options. If you'd like to see some implemented, open up an issue, fork, and create a PR!

# License

MIT / BSD

# Author Information

This role was created in 2021 by [Nick Herrig](nickherrig.com).
