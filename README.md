# ansible-role-rundeck
Ubuntu 14.04 LTS

## Synopsis

Install [rundeck](http://rundeck.org/)

## Requirements

- [Nginx](https://github.com/mats116/ansible-role-nginx)
- MySQL (Amazon RDS is recommended)

## Variables

| parameter | required | default | comments |
| --- | --- | --- | --- |
| rundeck_version | yes | 2.6.0 |  |
| rundeck_plugins | no | [3 plugins](https://github.com/mats116/ansible-role-rundeck/blob/master/defaults/main.yml#L3-L6) |  |
| framework_server_port | yes | 4440 |  | 
| framework_server_url | yes | http://localhost:4440 |  | 
| framework_server_username | yes | admin |  |
| framework_server_password | yes | admin |  |
| framework_ssh_keypath | yes | /var/lib/rundeck/.ssh/id_rsa |  | 
| framework_ssh_user | yes | rundeck |  | 
| framework_ssh_timeout | yes | 0 |  |
| rundeck_s3_bucket | no | Null |  |
| rundeck_s3_path | yes | logs/${job.project}/${job.id}/${job.execid}.log |  |
| rundeck_s3_region | yes | ap-northeast-1 |  |
| dataSource_dbCreate | yes | update |  |
| rundeck_clusterMode_enabled | yes | true |  |
| rd_mysql_host | yes | localhost |  |
| rd_mysql_database | yes | rundeck |  |
| rd_mysql_user | yes | rundeck |  |
| rd_mysql_password | yes | rundeck |  |
| mysql_root_user | no |  | If rd_mysql_host != localhost, it is required |
| mysql_root_password | no |  | If rd_mysql_host != localhost, it is required |
| rd_nginx_accesslog | yes | /var/log/nginx/rundeck-access.log |  |

## Examples

```yaml:paybook.yaml
- hosts: all
  sudo: yes
  roles:
    - role: rundeck
      framework_server_url: "https://rundeck.example.com"
      rd_mysql_host: rundeck.xxxxxxxxxxxx.ap-northeast-1.rds.amazonaws.com
      mysql_root_user: rds_admin
      mysql_root_password: rds_admin
```
