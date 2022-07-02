## Requirements

This role requires Ansible 2.4 or higher, and platform requirements are listed in the metadata file.

Currently, tests are done on:
- Centos 7
- Debian Stretch
- Ubuntu Xenial
- Ubuntu Bionic

and use:
- Ansible 2.4.x
- Ansible 2.5.x

Note: currently testing skips the idempotency checks, given work required to have Airflow database upgrades pass the Ansible requirements for idempotency.

## Role Variables

> **Warning**
> No Fernet key defined on configuration, so set your own before store passwords !

### Default role variables

This needs to be rewritten. Currently, see the `defaults/main.yml` for the variables expected for Airflow and Airflow Worker configurations.

## Dependencies

None

## Example Playbook

``` yaml
- hosts: airflow
  become: yes
  roles:
  - role: tulibraries.airflow
```

## License

MIT
