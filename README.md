[![CI](https://github.com/de-it-krachten/ansible-role-mariadb/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-mariadb/actions?query=workflow%3ACI)


# ansible-role-mariadb

Installs & configures MariaDB


Platforms
--------------

Supported platforms

- CentOS 7
- CentOS 8
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Debian 10 (Buster)
- Debian 11 (Bullseye)



Role Variables
--------------
<pre><code>


mariadb_release: 10.4
mariadb_pre_packages: []
mariadb_packages: []
mariadb_additional_packages: []
</pre></code>


Example Playbook
----------------

<pre><code>

- name: Converge
  hosts: all
  tasks:

    - name: "Include role 'ansible-role-mariadb'"
      include_role:
        name: "ansible-role-mariadb"
</pre></code>
