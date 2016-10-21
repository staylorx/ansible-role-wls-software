Role Name
=========

Installs the WLS software.

Requirements
------------

This presumes the wlsprep and java roles have been run. At least a JDK7 is required.

NOTE: The zip archives from Oracle are huge. Right now these copy from the files directory of the machine running Ansible. If the download_flag is set to true these will copy over. Otherwise, it is expected that the zips are already on the machine. Where I am I mount a shared folder and copy these to where they need to be.

Role Variables
--------------

```yaml
  oracle_user: oracle
  oracle_group: oinstall 
  java_home: /usr/java/latest
  oracle_base: /home/oracle
  mw_home: "{{ oracle_base }}/middleware"
  mw_installer_folder: "{{ oracle_base }}/installer"
```

There is some debate about where oracle binaries should go. This role does create the folder requiring root powers so an oracle_base of '/opt/oracle' is perfectly valid. It will be created as owned by the oracle_user.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

An example to install FMW Infrastructure and a colocated OHS:

```yaml
- hosts: admin
  become: yes
  become_user: oracle
  vars:
    download_flag: false
    oracle_installs:
      - { product: FMW_12.2.1.1.0, install_type: INFRA }
      - { product: OHS_12.2.1.1.0, install_type: COLOCATED }
  roles:
    - role: staylorx.wls-software
```

See the defaults/main.yml to see the code lists for products.

License
-------

MIT

