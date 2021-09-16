# Ansible Role: Nginx

[![MIT licensed][badge-license]][link-license]
[![Galaxy Role][badge-role]][link-galaxy]
[![Downloads][badge-downloads]][link-galaxy]

Installs [Nginx][nginx] on Linux and configure the service and template sites.

## Requirements

None.

## Role Variables

| Variable                           | Type         | Description                                             |
|:----------------------------------:|:------------:|:--------------------------------------------------------|
| `nginx_ssl_source_cert_path`       | string       | Path of the ssl certificate on Ansible master           |
| `nginx_ssl_source_key_path`        | string       | Path of the ssl key on Ansible master                   |
| `nginx_ssl_source_passphrase_path` | string       | Path of the ssl key passphrase on Ansible master        |
| `nginx_ssl_protocols`              | list(string) | List of protocols used for SSL/TLS                      |
| `nginx_ssl_ciphers`                | string       | List of ciphers used for SSL/TLS                        |
| `nginx_config_site_only`           | boolean      | Only run site config. Bypass Nginx service installation |
| `nginx_sites`                      | list(object) | List of site objects                                    |

### nginx_sites

This section explain how to configure an Nginx site.

Each `site` is defined with the following attributes :

| Variable  | Type     | Description                                    |
|:---------:|:--------:|:-----------------------------------------------|
| `enabled` | boolean  | Enable or not the site on the Nginx server     |
| `params`  | map(any) | Map of all parameters accepted in Nginx server |

## Dependencies

None.

## Example Playbook

    - hosts: localhost
      vars:
        nginx_ssl_source_cert_path: "/path/to/ssl/cert.crt"
        nginx_ssl_source_key_path: "/path/to/ssl/cert.key"
        nginx_ssl_source_passphrase_path: "/path/to/ssl/cert.passphrase"
        nginx_sites:
        - name: my-app
          enabled: yes
          params:
            server_name: "my-app.local"
            location:
              path: /
              params:
                proxy_pass: "http://127.0.0.1:5000"
        - name: my-app
          enabled: yes
          params:
            server_name: "my-app.local"
            root: /var/www/html
            index: index.html
            location:
              path: /
              params:
                try_files: "$uri $uri/ =404"
      roles:
        - lunik.nginx

## License

[MIT][link-license]

## Author Information

This role was created in 2019 by [Lunik (Guillaume MARTINEZ)][author-website].

#### Maintainer(s)

- [Lunik (Guillaume MARTINEZ)](https://github.com/Lunik)

[author-website]: https://lunik.tiwabbit.fr/
[badge-downloads]: https://img.shields.io/ansible/role/d/56259.svg
[badge-license]: https://img.shields.io/github/license/Lunik/ansible_role_nginx.svg
[badge-role]: https://img.shields.io/ansible/role/56259.svg
[link-galaxy]: https://galaxy.ansible.com/lunik/nginx
[link-license]: https://raw.githubusercontent.com/Lunik/ansible_role_nginx/master/LICENSE
[nginx]: https://www.nginx.com
