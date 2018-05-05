# Wordpress ansible

This role deploys an engelsystem instance 


## Requirements

This role requires the [php-fpm role](https://github.com/stuvusIT/php-fpm), the [nginx role](https://github.com/stuvusIT/nginx) and the [maria db role](https://github.com/stuvusIT/mariadb)

## Role Variables

### General

| Name                                  | Required/Default                                             | Description                                                            |
|---------------------------------------|:------------------------------------------------------------:|------------------------------------------------------------------------|
| `engelsystem_user`                    | `www-data`                                                   | User under which the files for the engelsystem should be held          |
| `engelsystem_group`                   | `www-data`                                                   | Group under which the files for the engelsystem should be held         |
| `engelsystem_install_path`            | `/opt/engelsystem`                                           | Path where the engelsystem should be install to                        |
| `engelsystem_version`                 | `master`                                                     | Version which should be checkout during the installation               |
| `engelsystem_mysql_host`              | `localhost`                                                  | Host address where the mysql database runs                             |
| `engelsystem_mysql_user`              | `engelsystem`                                                | User for the mysql instance                                            |
| `engelsystem_mysql_password`          | :heavy_check_mark:                                           | Password for the mysql user                                            |
| `engelsystem_mysql_database`          | `engelsystem`                                                | Databasename                                                           |
| `engelsystem_api_key`                 | `''`                                                         | API key for accessing stats                                            |
| `engelsystem_maintenance`             | `false`                                                      | Enable maintenance mode                                                |
| `engelsystem_environment`             | `production`                                                 | Set to development to enable debugging messages                        |
| `engelsystem_faq_url`                 | `https://events.ccc.de/congress/2013/wiki/Static:Volunteers` | URL to the angel faq and job description                               |
| `engelsystem_contact_email`           | `contact@engelsystem.de`                                     | Contact email address, linked on every page                            |
| `engelsystem_no_reply_email`          | `noreply@engelsystem.de`                                     | From address of all emails                                             |
| `engelsystem_theme`                   | `1`                                                          | Default theme, 1=style1.css                                            |
| `engelsystem_display_news`            | `6`                                                          | Number of News shown on one site                                       |
| `engelsystem_registration_enabled`    | `false`                                                      | Users are able to sign up                                              |
| `engelsystem_signup_requires_arrival` | `false`                                                      | Only arrived angels can sign up for shifts                             |
| `engelsystem_last_unsubscribe`        | `24`                                                         | Number of hours before a shit where it is still possible to unregister |
| `engelsystem_crypt_alg`               | `'$6$rounds=5000'`                                           | Crypto Algorithm used for crypt                                        |
| `engelsystem_min_password_length`     | `6`                                                          | Minimum number of characters for a password                            |
| `engelsystem_enable_tshirt_size`      | `true`                                                       | Enable to ask angels during singup for their tshirt size               |
| `engelsystem_freeloadable_shifts` | `2`                                                          | Number of shifts to freeload until angel is locked for shift signup.   |
| `engelsystem_timezone`                | `'Europe/Berlin'`                                            | Local timezone                                                         |
| `engelsystem_shift_sum_formula`       | `'SUM(\`end\` - \`start\`)'`                                 | SQL Formula used to calculate shift weights                            |
| `engelsystem_default_locale`          | `'de_DE.UTF-8'`                                              | Default locale to use for each user                                    |
| `engelsystem_tshirt_sizes`            | [See the defaults.yml](defaults/main.yml)                    | Dict of tshirt sizes                                                   |
| `engelsystem_themes`                  | [See the defaults.yml](defaults/main.yml)                    | List of avaliable themes                                               |
| `engelsystem_voucher_settings`        | [See the defaults.yml](defaults/main.yml)                    | Dict with voucher settings                                             |
| `engelsystem_locales`                 | [See the defaults.yml](defaults/main.yml)                    | Dict with locales mapped to language                                   |

## Example Playbook

```yml
- hosts: wordpress
  roles:
    - role: wordpress
      wordpress_mysql_password: password
      wordpress_default_password: password
      wordpress_default_email: admin@example.com
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).


## Author Information

 * [Fritz Otlinghaus(Scriptkiddi)](https://github.com/Scriptkiddi) _fritz.otlinghaus@stuvus.uni-stuttgart.de_
