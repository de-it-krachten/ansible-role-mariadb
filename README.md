[![CI](https://github.com/de-it-krachten/ansible-role-mariadb/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-mariadb/actions?query=workflow%3ACI)


# ansible-role-mariadb

Installs & configures MariaDB 10.x using packages from mariadb.com


## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- AlmaLinux 8
- Debian 11 (Bullseye)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# MariaDB packages
mariadb_pre_packages: []
mariadb_packages: []
mariadb_additional_packages: []

# Shoud socket authentication be used
mariadb_socket_authentication: true

# Mariadb DB settings
mariadb_db_name: ''
mariadb_db_delete: false

# innodb
mariadb_innodb:
  innodb_buffer_pool_size: 1G
  innodb_log_file_size: 64M
  innodb_lock_wait_timeout: 900
</pre></code>

### defaults/family-RedHat.yml
<pre><code>
# MariaDB version
mariadb_release: 10.4

# List of MariaDB package it depends on
mariadb_pre_packages:
  - epel-release

# List of MariaDB package
mariadb_packages:
  - python3-mysql
  - MariaDB-server
  - MariaDB-backup
  - galera-4

# Configuration path
mariadb_config_dir: /etc/my.cnf.d

# UNIX socket for authentication
mariadb_socket: /var/lib/mysql/mysql.sock
</pre></code>

### defaults/family-Debian.yml
<pre><code>
# MariaDB version
mariadb_release: 10.4

# List of MariaDB package it depends on
mariadb_pre_packages:
  - apt-transport-https
  - software-properties-common
  - python3-pymysql
  - rsync

# List of MariaDB package
mariadb_packages:
  - mariadb-server
  - mariadb-client
  - mariadb-backup

# Configuration path
mariadb_config_dir: /etc/mysql/conf.d

# UNIX socket for authentication
mariadb_socket: /var/run/mysqld/mysqld.sock
</pre></code>

### defaults/Debian-11.yml
<pre><code>
# MariaDB version
mariadb_release: 10.8
</pre></code>

### defaults/Ubuntu-22.yml
<pre><code>
# MariaDB version
mariadb_release: 10.8
</pre></code>

### defaults/family-RedHat-9.yml
<pre><code>
# MariaDB version
mariadb_release: 10.8

# List of MariaDB package
mariadb_packages:
  - python3-mysqlclient
  - MariaDB-server
  - MariaDB-backup
  - galera-4
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'mariadb'
  hosts: all
  become: "{{ molecule['converge']['become'] | default('yes') }}"
  vars:
    mariadb_user: root
    mariadb_pwd: root1234
    mariadb_db_name: db01
    mariadb_db_user: user01
    mariadb_socket_authentication: True
  tasks:
    - name: Include role 'mariadb'
      include_role:
        name: mariadb
</pre></code>
