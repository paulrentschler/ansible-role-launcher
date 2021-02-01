paulrentschler.launcher
=======================

Install and configure the SSH connection/tunnel launcher script


Requirements
------------

None.


Role Variables
--------------

The following variables are available with defaults defined in `defaults/main.yml`:

Specify the parent directory for the Launcher script.

    launcher_parent_dir: "/usr/local/scripts"

Specify the directory that the Launcher script will be cloned into.

    launcher_install_dir: "{{ launcher_parent_dir }}/launcher"

Configure the launcher script with hosts from the Ansible inventory. By default it will include all of the hosts but you can also specify a list of specific hosts you want to configure from the Ansible inventory.

    launcher_inventory_hosts: "{{ groups['all'] }}"

Specify servers for the launcher configuration.

    launcher_hosts: []

An example of how this varible would be defined:

    launcher_servers:
      - nickname1:
          fqdn: host1.example.com
          ip: 192.168.10.1
          port: 2222


Dependencies
------------

By default the parent directory for the launcher script and the cloned repo with the launcher script will be owned by the `devops_user` variable if defined, otherwise `ansible_user` by default.

The group will be `devops_group` if defined, otherwise `adm` by default.


Example Playbook
----------------

Simpliest example that uses defaults to install and configure the launcher with all of the Ansible inventory hosts.

    - hosts: all
      roles:
        - paulrentschler.launcher

Install the launcher script but **do not** configure the Ansible inventory hosts.

    - hosts: all
      roles:
        - role: paulrentschler.launcher
          vars:
            launcher_inventory_hosts: []

Install the launcher script, configure some of the Ansible inventory hosts, and specify additional hosts.

    - hosts: all
      roles:
        - role: paulrentschler.launcher
          vars:
            launcher_inventory_hosts:
              - host1
              - host5
            launcher_hosts:
              - nickname1:
                  fqdn: host1.example.com
                  ip: 192.168.10.1
                  port: 2222
              - nickname2:
                  ip: 192.168.10.15


License
-------

MIT


Author Information
------------------

Created by Paul Rentschler in 2021.
