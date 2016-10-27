Firewall
========

Ansible role for managing firewall on RedHat and Debian based distros. Only `ferm` firewall is supported at the moment.

Requirements
------------

Requires the EPEL repository on RedHat/CentOS (you can install it by simply adding the `geerlingguy.repo-epel` role to your playbook).
Mentioned `geerlingguy.repo-epel` role can be installed from Galaxy:

    ansible-galaxy install geerlingguy.repo-epel

Role Variables
--------------

The  variables should be configured by the user (default values provided) :

* ``fw_tool``: Select firewall (string, currently only ``ferm`` is supported and is default by chance)
* ``fw_force_restart``: Re-apply firewall config file even if it will not be changed (boolean, default: ``false``)
* ``fw_profile``: Select firewall profile/template (string, default: ``ssh_only``)

Firewall profile is searched in the following locations (with first found applied):

    - "{{ playbook_dir }}/templates/{{ inventory_hostname }}_ferm.{{ fw_profile }}.conf.j2"
    - "{{ playbook_dir }}/templates/ferm.{{ fw_profile }}.conf.j2"
    - "{{ role_path }}/templates/ferm.{{ fw_profile }}.conf.j2"


Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - name: Configure firewall
      hosts: all
      become: yes
      roles:
        - role: firewall
          fw_force_restart: true

License
-------

BSD

Author Information
------------------

The role was created by VA some time ago, refactored in Oct 2016.

