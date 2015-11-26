# README.md
# Ansible Role: mats116.rundeck

An Ansible role that configure [Rundeck](http://rundeck.org/) on **Ubuntu 14.04 LTS**

## Requirements

none

## Role Variables

Available variables are listed below, along with default values:

```yaml
rundeck_version: "2.6.0"

rundeck_plugins:
  - "https://github.com/rundeck-plugins/rundeck-ec2-nodes-plugin/releases/download/v1.5.1/rundeck-ec2-nodes-plugin-1.5.1.jar"
  - "https://github.com/rundeck-plugins/rundeck-s3-log-plugin/releases/download/v1.0.0/rundeck-s3-log-plugin-1.0.0.jar"
  - "https://github.com/higanworks/rundeck-slack-incoming-webhook-plugin/releases/download/v0.3.dev/rundeck-slack-incoming-webhook-plugin-0.3.jar"

# framework.properties
framework_server_port: 4440
framework_server_url: "http://localhost:4440"
framework_server_username: admin
framework_server_password: admin

framework_ssh_keypath: /var/lib/rundeck/.ssh/id_rsa
framework_ssh_user: rundeck
framework_ssh_timeout: 0

rundeck_s3_bucket: ""
rundeck_s3_path: "logs/${job.project}/${job.id}/${job.execid}.log"
rundeck_s3_region: ap-northeast-1

# rundeck-config.properties
dataSource_dbCreate: update
rundeck_clusterMode_enabled: "true"

# MySQL
rd_mysql_host: localhost
rd_mysql_database: rundeck
rd_mysql_user: rundeck
rd_mysql_password: rundeck

# Nginx
rd_nginx_accesslog: /var/log/nginx/rundeck-access.log
```

## Dependencies

- [mats116.nginx](https://galaxy.ansible.com/detail#/role/6198) - Installer of Nginx
- [mats116.java8](https://galaxy.ansible.com/detail#/role/6197) - Installer of Java8
- [mats116.mariadb-server](https://galaxy.ansible.com/detail#/role/6199) - Installer of MariaDB Server (MySQL)
 - `when "rd_mysql_host == 'localhost'"`

## Example Playbook

```yaml
- hosts: rundeck-server
  roles:
    - role: mats116.rundeck
      framework_server_url: "https://rundeck.example.com"
      rd_mysql_host: rundeck.xxxxxxxxxxxx.ap-northeast-1.rds.amazonaws.com
      mysql_root_user: rds_admin
      mysql_root_password: rds_admin
```

## License

MIT
