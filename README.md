[![CI](https://github.com/de-it-krachten/ansible-role-mariadb/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-mariadb/actions?query=workflow%3ACI)


# ansible-role-mariadb

Installs & configures MariaDB 10.x using packages from mariadb.com


Platforms
--------------

Supported platforms

- RHEL 8
- CentOS 8
- RockyLinux 8
- AlmaLinux 8
- Ubuntu 20.04 LTS

Note:
<sup>1</sup> : no automated testing is performed on these platforms

Role Variables
--------------
<pre><code>
# MariaDB version
mariadb_release: 10.4

# MariaDB packages
mariadb_pre_packages: []
mariadb_packages: []
mariadb_additional_packages: []

# innodb
mariadb_innodb:
  innodb_buffer_pool_size: 1G
  innodb_log_file_size: 64M
  innodb_lock_wait_timeout: 900
</pre></code>


Example Playbook
----------------

<pre><code>
- name: sample playbook for role 'mariadb'
  hosts: all
  vars:
    mariadb_db_name: db01
    mariadb_db_user: user01
  tasks:
    - name: Include role 'mariadb'
      include_role:
        name: mariadb
</pre></code>
