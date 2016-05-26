Role Name
=========

Installs the WLS software.

Requirements
------------

This presumes the wlsprep and java roles have been run. At least a JDK7 is required.

NOTE: The zip archives from Oracle are huge. Right now these copy from the files directory of the machine running Ansible. If the download_flag is set to true these will copy over. Otherwise, it is expected that the zips are already on the machine. Where I am I mount a shared folder and copy these to where they need to be.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

An example to install FMW Infrastructure, a colocated OHS, and the EDQ binaries:

```yaml
- hosts: admin
  become: yes
  become_user: oracle
  vars:
    download_flag: false
    oracle_installs:
      - FMW,EXAMPLES
      - OHS,COLOCATED
      - EDQ,WEBLOGIC
  roles:
    - role: staylorx.wls-software
```

See the defaults/main.yml to see the code lists for products.

License
-------

MIT

