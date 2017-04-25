# Ansible Role: Configure Ansible

An ansible role to configure ansible.

## Requirements

> This role has been tested on `Ubuntu 16.04` and `Ubuntu 16.10` only.

## Variables

- `configure_ansible_config_directory`: configuration directory.
  - Default: `/etc/ansible`

- `configure_ansible_config_items`: configuration items by section.
  - Default:
  ```yaml
    defaults: []
    privilege_escalation: []
    paramiko_connection: []
    ssh_connection: []
    accelerate: []
    selinux: []
    colors: []
    diff: []
  ```

- `configure_ansible_vault_password`: vault password. set this value to create a vault password file.
  - Default: `[undefined]`
  > **NOTE**: setting this value only creates the vault password file.
  >
  > You will need to configure ansible to look here by setting the `vault_password_file` option under `configure_ansible_config_defaults`.
  >
  > If the default file permissions are used, you will need to run `ansible` commands as `sudo`, the defined `owner` or `group` member. Ansible exits with `ERROR! The vault password file /path/to/vault/file was not found` otherwise.


- `configure_ansible_vault_password_file`: vault password file attributes.
  - Default:
  ```yaml
    path: /etc/ansible/.vpf # path to password file.
    owner: root # owner of the password file.
    group: root # group of the password file.
    permissions: 0640 #  unix permissions to apply to the password file. fed to `chmod`.
  ```

- `configure_ansible_install_apt`: additional apt packages to install.
  - Default:
    - `python-passlib`
    - `python-pip`
- `configure_ansible_install_pip`: additional pip libraries to install.
  - Default:
    - `cryptography`

### Configuration Items Definition

`configure_ansible_config_items` is is a dictionary of `sections` and each `section a list of dictionaries that should conform to the following definition.

- `name`: the configuration name. e.g. `inventory`
  - **Required**

- `value`: the configuration value. e.g `etc/ansible/hosts`.
  - **Required**

You can find a documented list of [configuration values here](files/ansible.cfg).

## Usage Example

```yaml
- hosts: all
  vars:
    configure_ansible_vault_password: "pa55w0rd"
    configure_ansible_vault_password_file:
      path: /etc/ansible/vault.pass
    configure_ansible_config_items:
      defaults:
        - { name: "host_key_checking", value: "False" }
        - { name: "ansible_managed", value: "DO NOT MODIFY by hand. This file is under control of Ansible on {host}." }
        - { name: "vault_password_file", value: "/path/to/vault/file" }
      accelerate:
        - { name: "accelerate_port", value: "5099" }
  roles:
    - thedumbtechguy.configure-ansible
```


## License

MIT / BSD

## Author Information

This role was created by [TheDumbTechGuy](https://github.com/thedumbtechguy) ( [twitter](https://twitter.com/frostymarvelous) | [blog](https://thedumbtechguy.blogspot.com) | [galaxy](https://galaxy.ansible.com/thedumbtechguy/) )

## Credits