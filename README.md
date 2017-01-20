[![Build
Status](https://img.shields.io/travis/lafarer/ansible-role-do-droplets.svg)](https://travis-ci.org/lafarer/ansible-role-do-droplets)
[![License](https://img.shields.io/github/license/lafarer/ansible-role-do-droplets.svg)](https://github.com/lafarer/ansible-role-do-droplets/blob/master/LICENSE)
[![Galaxy](http://img.shields.io/badge/galaxy-lafarer.digitalocean--droplet-blue.svg)](https://galaxy.ansible.com/lafarer/do-droplets/)

# Ansible role: lafarer.do-droplets

Ansible role to create and bootstrap digitalocean droplet(s).

if `do_inventory_file` is set the created droplets are added to the `[digitalocean]` section of the inventory file.

During droplet creation, minimal security update is applied:
    - SSH - Key based login, disable root login and change port
    - Protect su by limiting access only to droplet admin user

## Requirements

*   Ansible 2.2
*   Two environment variables can be used, DO_API_KEY and DO_API_TOKEN. They both refer to the v2 token.

## Installation

Using `ansible-galaxy`:

```shell
  $ ansible-galaxy install lafarer.do-droplets
```

Using `requirements.yml`:

```yaml
  - src: lafarer.do-droplets
```

Using `git`:

```shell
  $ git clone https://github.com/lafarer/ansible-role-do-droplets.git lafarer.do-droplets
```
## Role Variables

```yaml
  ---
  # The public SSH keys you want to add to your account.
  # do_keys:
  #   - name: mykey                             # The name of a SSH key
  #     pub_key_file: "~/.ssh/id_rsa.pub"       # The public SSH key file
  do_keys: []

  # Droplets to be created
  # do_droplets:
  #   backups_enabled:    no                    # Boolean, enables backups for your droplet.
  #   image_id:           ubuntu-16-04-x64      # This is the slug of the image you would like the droplet created with.
  #   name:               mydroplet             # The name of the droplet. Must be unique.
  #   port:               22                    # SSH port
  #   private_networking: no                    # Boolean, add an additional, private network interface to droplet for inter-droplet communication.
  #   region_id:          fra1                  # This is the slug of the region you would like your server to be created in.
  #   size_id:            512mb                 # This is the slug of the size you would like the droplet created with.
  #   ssh_key_name:       mykey                 # SSH key name (defined in do_keys)
  #   user:               lookup('env', 'USER') # Admin user to create
  #   virtio:             yes                   # Boolean, turn on virtio driver in droplet for improved network and storage I/O.
  #   wait:               yes                   # Wait for the droplet to be in state 'running' before returning.
  #   wait_timeout:       600                   # How long before wait gives up, in seconds.
  #
  do_droplets: []

  # Inventory file to update
  do_inventory_file:
  # Hosts file to update
  do_hosts_file: /etc/hosts
```

## Dependencies

## Example Playbook

Create your own Playbook

```yaml
  - name: Provision DigitalOcean droplets
    hosts: localhost
    gather_facts: no
    vars:
      do_keys:
        - name: admin@example.com
          pub_key_file: "~/.ssh/id_rsa.pub"
      do_droplets:
        - name: example.com
          port: 4222
          user: admin
          ssh_key_name: admin@example.com
      do_inventory_file: ~/.ansible/hosts

    roles:
      - lafarer.do-droplets
```

## License

MIT
