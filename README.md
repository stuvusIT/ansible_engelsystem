# engelsystem

This role deploys an [Engelsystem](https://engelsystem.de) instance.


## Requirements

Debian stretch or newer.
Additionally, [PHP-FPM](https://github.com/stuvusIT/php-fpm), [nginx](https://github.com/stuvusIT/nginx), and [MariaDB](https://github.com/stuvusIT/mariadb) are required.

## Role Variables

### General

| Name                         | Required/Default                             | Description                                                                                                                                                                                                          |
|------------------------------|:--------------------------------------------:|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `engelsystem_user`           | `www-data`                                   | User which owns the writable Engelsystem files (import and storage)                                                                                                                                                  |
| `engelsystem_group`          | `www-data`                                   | Group which owns the writable Engelsystem files (import and storage)                                                                                                                                                 |
| `engelsystem_install_path`   | `/opt/engelsystem`                           | Path where the engelsystem should be installed to                                                                                                                                                                    |
| `engelsystem_repo`           | `https://github.com/engelsystem/engelsystem` | URL of the repository to clone                                                                                                                                                                                       |
| `engelsystem_version`        | `master`                                     | Version which should be checked out during the installation                                                                                                                                                          |
| `engelsystem_mysql_host`     | `localhost`                                  | Host address where the MariaDB database runs                                                                                                                                                                         |
| `engelsystem_mysql_user`     | `engelsystem`                                | User for the MariaDB instance                                                                                                                                                                                        |
| `engelsystem_mysql_password` | :heavy_check_mark:                           | Password for the MariaDB user                                                                                                                                                                                        |
| `engelsystem_mysql_database` | `engelsystem`                                | Database name for the MariaDB database                                                                                                                                                                               |
| `engelsystem_remove_privs`   | `[]`                                         | Remove these privileges from all Engelsystem user groups                                                                                                                                                             |
| `engelsystem_admin_password` | [`asdfasdf` in SHA-512]                      | Password for the admin user in `crypt(3)` format. Set to an empty string to leave as-is                                                                                                                              |
| `engelsystem_config`         |                                              | Dict to set [config.php](https://github.com/engelsystem/engelsystem/blob/master/config/config.default.php) values. Dicts and lists will be expanded and strings will be quoted and their special characters esacped. |

## Example Playbook

```yml
- hosts: engelsystem
  roles:
    - role: engelsystem
      engelsystem_mysql_password: pleasechangethis
      engelsystem_remove_privs:
        - user_messages
      engelsystem_config:
        enable_tshirt_size: False
        default_locale: de_DE.UTF-8
        night_shifts:
          enabled: False
          start: 2
          end: 6
          multiplier: 2

      served_domains:
        - domains:
          - helfer.campusbeach.stuvus.uni-stuttgart.de.
          https: true
          crypto: true
          root: /opt/engelsystem/public
          privkey_path: /etc/ssl/privkey.pem
          fullchain_path: /etc/ssl/fullchain.pem
          default_server: true
          allowed_ip_ranges:
            - 129.69.139.0/25
          index_files:
            - index.php
          locations:
            - condition: /
              content: try_files $uri $uri/ /index.php?$args;
            - condition: ~ \.php$
              content: include fastcgi.conf; fastcgi_intercept_errors on; fastcgi_pass unix:/run/php/php7.0-fpm.sock;
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

 * [Fritz Otlinghaus(Scriptkiddi)](https://github.com/Scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
