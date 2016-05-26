Role Name
=========

Installs the WLS software.

Requirements
------------

This presumes the wlsprep and java roles have been run. At least a JDK7 is required.


Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

An example to install FMW Infrastructure, a colocated OHS, and the EDQ binaries:

- hosts: admin
  become: yes
  become_user: oracle
  vars:
    #download_flag: false
    cleanup_flag: false
    oracle_installs:
      - FMW,EXAMPLES
      - OHS,COLOCATED
      - EDQ,WEBLOGIC
  roles:
    - role: staylorx.wls-software

See the defaults/main.yml to see the code lists for products.

License
-------

MIT

