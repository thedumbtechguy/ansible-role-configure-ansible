# Ansible Role: Configure Self

An ansible role to configure ansible.

## Requirements

> This role has been tested on `Ubuntu 16.04` and `Ubuntu 16.10` only.

## Variables

- `configure_self_config_directory`: configuration directory.
  - Default: `/etc/ansible`

- `configure_self_config_defaults`: configuration relating to the `defaults` section.
  - Default: `[]`
- `configure_self_config_privilege_escalation`: configuration relating to the `privilege_escalation` section.
  - Default: `[]`
- `configure_self_config_paramiko_connection`: configuration relating to the `paramiko_connection` section.
  - Default: `[]`
- `configure_self_config_ssh_connection`: configuration relating to the `ssh_connection` section.
  - Default: `[]`
- `configure_self_config_accelerate`: configuration relating to the `accelerate` section.
  - Default: `[]`
- `configure_self_config_selinux`: configuration relating to the `selinux` section.
  - Default: `[]`
- `configure_self_config_colors`: configuration relating to the `colors` section.
  - Default: `[]`
- `configure_self_config_diff`: configuration relating to the `diff` section.
  - Default: `[]`


- `configure_self_vault_password`: vault password. set this value to create a vault password file.
  - Default: `[undefined]`
- `configure_self_vault_password_file`: vault password file.
  - Default: `/etc/ansible/.vpf`
  > **NOTE**: setting this value only creates the vault password file.
  >
  > You will need to configure ansible to look here by setting the `vault_password_file` option under `configure_self_config_defaults`.
  >
  > If the default file permissions are used, you will need to run `ansible` commands as `sudo`, the defined `owner` or `group` member. Ansible exits with `ERROR! The vault password file /path/to/vault/file was not found` otherwise.

- `configure_self_vault_password_file_owner`: owner of the password file.
  - Default: `root`
- `configure_self_vault_password_file_group`: group of the password file.
  - Default: `root`
- `configure_self_vault_password_file_permissions`: unix permissions to apply to the password file. fed to `chmod`.
  - Default: `0644`

- `configure_self_install_apt`: additional apt packages to install.
  - Default:
    - `python-passlib`
    - `python-pip`
- `configure_self_install_pip`: additional pip libraries to install.
  - Default:
    - `cryptography`

### Configuration Definition

Each configuration in the list should conform to the following definition.

- `name`: the configuration name. e.g. `inventory`
  - **Required**

- `value`: the configuration value. e.g `etc/ansible/hosts`.
  - **Required**

You can find a documented list of [configuration values here](files/ansible.cfg).

## Usage Example

```yaml
- hosts: all
  vars:
    configure_self_config_defaults:
      - name: host_key_checking
        value: False
      - name: ansible_managed
        value: 'DO NOT MODIFY by hand. This file is under control of Ansible on {host}.'
      - name: vault_password_file
        value: /path/to/vault/file
  roles:
    - thedumbtechguy.configure-self
```


## License

MIT / BSD

## Author Information

This role was created by [Stefan Froelich](https://thedumbtechguy.blogspot.com/).

## Credits