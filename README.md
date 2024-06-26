[![CI](https://github.com/de-it-krachten/ansible-role-mariadb/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-mariadb/actions?query=workflow%3ACI)


# ansible-role-mariadb

Installs & configures MariaDB 10.x using packages from mariadb.com



## Dependencies

#### Roles
None

#### Collections
- community.general
- community.mysql

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- OracleLinux 9
- AlmaLinux 8
- AlmaLinux 9
- SUSE Linux Enterprise 15<sup>1</sup>
- openSUSE Leap 15
- Debian 11 (Bullseye)
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Ubuntu 24.04 LTS

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# MariaDB version
# mariadb_release: '10.11'

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

### defaults/Debian-11.yml
<pre><code>

</pre></code>

### defaults/family-Debian.yml
<pre><code>
# Package repository to use
mariadb_repo: >-
  https://downloads.mariadb.com/MariaDB/mariadb-{{ mariadb_release }}/repo/{{ ansible_distribution | lower }}

# GPG key
mariabdb_gpg_key: >-
  https://downloads.mariadb.com/MariaDB/MariaDB-Server-GPG-KEY

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

### defaults/family-RedHat-7.yml
<pre><code>
# List of MariaDB package
mariadb_packages:
  - python3-mysql
  - MariaDB-server
  - MariaDB-backup
  - galera-4
</pre></code>

### defaults/family-RedHat-8.yml
<pre><code>
# List of MariaDB package
mariadb_packages:
  - python3-mysql
  - MariaDB-server
  - MariaDB-backup
  - galera-4
</pre></code>

### defaults/family-RedHat-9.yml
<pre><code>
# List of MariaDB package
mariadb_packages:
  - python3-mysqlclient
  - MariaDB-server
  - MariaDB-backup
  - galera-4
</pre></code>

### defaults/family-RedHat.yml
<pre><code>
# Package repository to use
mariadb_repo: >-
  https://downloads.mariadb.com/MariaDB/mariadb-{{ mariadb_release }}/yum/rhel/$releasever/$basearch

# GPG key
mariabdb_gpg_key: >-
  https://downloads.mariadb.com/MariaDB/RPM-GPG-KEY-MariaDB

# List of MariaDB package it depends on
mariadb_pre_packages:
  - epel-release

# Configuration path
mariadb_config_dir: /etc/my.cnf.d

# UNIX socket for authentication
mariadb_socket: /var/lib/mysql/mysql.sock
</pre></code>

### defaults/family-Suse-15.yml
<pre><code>
# List of MariaDB package
mariadb_packages:
  - python3-mysqlclient
  - MariaDB-server
  - MariaDB-backup
  - galera-4
</pre></code>

### defaults/family-Suse.yml
<pre><code>
# Package repository to use
mariadb_repo: >-
  https://downloads.mariadb.com/MariaDB/mariadb-{{ mariadb_release }}/yum/opensuse/$releasever_major/$basearch

# GPG key
mariabdb_gpg_key: >-
  https://downloads.mariadb.com/MariaDB/MariaDB-Server-GPG-KEY

# List of MariaDB package it depends on
mariadb_pre_packages: []

# Configuration path
mariadb_config_dir: /etc/my.cnf.d

# UNIX socket for authentication
mariadb_socket: /var/lib/mysql/mysql.sock
</pre></code>

### defaults/Ubuntu-22.yml
<pre><code>

</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'mariadb'
  hosts: all
  become: 'yes'
  vars:
    mariadb_release: 10.11
    mariadb_user: root
    mariadb_pwd: root1234
    mariadb_db_name: db01
    mariadb_db_user: user01
    mariadb_socket_authentication: true
  tasks:
    - name: Include role 'mariadb'
      ansible.builtin.include_role:
        name: mariadb
</pre></code>
