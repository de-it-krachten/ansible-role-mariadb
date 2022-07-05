[![CI](https://github.com/de-it-krachten/ansible-role-mariadb/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-mariadb/actions?query=workflow%3ACI)


# ansible-role-mariadb

Installs & configures MariaDB 10.x using packages from mariadb.com


## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- OracleLinux 8
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
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

### vars/Debian.yml
<pre><code>
mariadb_pre_packages:
  - apt-transport-https
  - software-properties-common
  - python3-pymysql
  - rsync
mariadb_packages:
  - mariadb-server
  - mariadb-client
  - mariadb-backup

mariadb_config_dir: /etc/mysql/conf.d
mariadb_socket: /var/run/mysqld/mysqld.sock
</pre></code>

### vars/RedHat.yml
<pre><code>
mariadb_pre_packages:
  - epel-release
mariadb_packages:
  - python3-mysql
  - MariaDB-server
  - MariaDB-backup
  - galera-4

mariadb_config_dir: /etc/my.cnf.d
mariadb_socket: /var/lib/mysql/mysql.sock
</pre></code>



## Example Playbook
### molecule/default/converge.yml
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
