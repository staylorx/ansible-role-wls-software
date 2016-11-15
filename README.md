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

Need to install OSB 12c? From Oracle's cloud delivery site with the V-zip names and all? Here the download flag is set to no and the mw_software_folder is set to indicate where the software can be found. It's put there separately. Note that the oracle_products hash overrides the defaults entirely.
```
- hosts: weblogic
  become: yes
  become_user: oracle
  vars:
    download_flag: no
    mw_software_folder: /osbdev/software
    oracle_products:
      FMW_12.2.1.2.0:
        install_zips:
          - V779122-01.zip
        install_binary:  fmw_12.2.1.2.0_infrastructure.jar
        binary_type:     jar
        create_artifact: wlserver
        INFRA:           Fusion Middleware Infrastructure
        EXAMPLES:        Fusion Middleware Infrastructure With Examples
      OHS_12.2.1.2.0:
        install_zips:
          - V789368-01.zip
        install_binary:  fmw_12.2.1.2.0_ohs_linux64.bin
        binary_type:     bin
        create_artifact: ohs
        COLOCATED:       Collocated HTTP Server (Managed through WebLogic server)
        STANDALONE:      Standalone HTTP Server (Managed independently of WebLogic server)
      OSB_12.2.1.2.0:
        install_zips:
          - V779126-01.zip
        install_binary:  fmw_12.2.1.2.0_osb.jar
        binary_type:     jar
        create_artifact: osb
        SERVICEBUS:      Service Bus
    oracle_installs:
      - { product: FMW_12.2.1.2.0, install_type: INFRA }
      - { product: OSB_12.2.1.2.0, install_type: SERVICEBUS }
      - { product: OHS_12.2.1.2.0, install_type: COLOCATED }
  roles:
    - role: staylorx.wls-software
```

License
-------

MIT

