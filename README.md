[![Build Status](https://travis-ci.org/RuntimeLLC/ansible_postgresql.svg?branch=master)](https://travis-ci.org/RuntimeLLC/ansible_postgresql)

#PostgreSQL Server

Example of the role of inclusion:
```
- hosts: database
  become: yes
  become_method: sudo
  roles:
    - role: postgresql
      pg_users:
        - name: 'test1'
        - name: 'test2'
          pass: 'test2_password'
        - name: 'test3'
          pass: 'test3_password'
          role_attr_flags: 'LOGIN'
      pg_databases:
        - name: 'test1'
        - name: 'test2'
          owner: 'test2'
        - name: 'test3'
          encoding: 'UTF-8'
          lc_collate: 'en_US.UTF-8'
          lc_ctype: 'en_US.UTF-8'
          owner: 'test3'
          extensions: 
            - "pg_buffercache"
            - "pg_stat_statements"
      pg_hba_settings:
        - { value: 'host test1 postgres 127.0.0.1/32 md5'}
        - { value: 'host test2 postgres 127.0.0.1/32 md5', state: 'present' }
        - { value: 'host test2 test2 192.168.122.0/24 md5' }
        - { value: 'host test3 test2 192.168.100.0/24 md5', state: 'absent'}
      pg_settings:
        - { name: 'listen_addresses', value: '*' }
        - { name: 'lc_messages', value: 'en_US.UTF-8' }
        - { name: 'log_line_prefix', value: '%t [%p]: [%l-1] ' }
        - { name: 'log_temp_files', value: '0', state: 'absent' }
```
