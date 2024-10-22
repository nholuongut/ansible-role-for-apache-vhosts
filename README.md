# Ansible Role: Apache vhosts
![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

## Purpose

nholuong.nginx manage sites in separate files and role supporting explicitly remove sites.


Role vianholuongsite-ansible.site does complex site setup: user creation, setup nginx, apache, mysql etc. Each site plays as separate role,
so I need for separate apache vhosts too.

This role allow of using nholuong.apache other way.

Other roles "apache-vhosts" that I found doing same that nholuong-ansible.site: it too complex.


## Features
- Add sites with several playbooks
- Explicitly remove sites
- Each site can have separate template


## Limitations
- only Debian, Ubuntu and CentOS
- no SSL (we confifuring SSL on nginx)

Issues welcome!


## Usage

Before this role you must install apache with geerlingguy.apache role or other way.

Some variables names and values matches geerlingguy's role (see default and vars directories). So, you can don't define it twice.

### Add sites:

Site definition matches close too:

```yaml
apache_vhosts_sites:
  www.local.dev:
    servername: "www.local.dev"
    serveralias: "local.dev"
    documentroot: "/var/www/html"
    extra_parameters: |
      RewriteCond %{HTTP_HOST} !^www\. [NC]
      RewriteRule ^(.*)$ http://www.%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

Compared with geerlingguy's:

```yaml
apache_vhosts_sites:
  - servername: "www.local.dev"
    serveralias: "local.dev"
    documentroot: "/var/www/html"
    extra_parameters: |
      RewriteCond %{HTTP_HOST} !^www\. [NC]
      RewriteRule ^(.*)$ http://www.%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
```

#### Custom template for site:

```yaml
apache_vhosts_sites:
  www.local.dev:
    servername: "www.local.dev"
    template: "custom.conf.j2"
```

### Remove sites:

```yaml
apache_vhosts_remove_sites:
  - www.local.dev
```


## Example Playbook

```yaml
- hosts: all
  roles:
    - nholuong-ansible.apache-vhosts
  vars:
    apache_vhosts_sites:
      foo:
        servername: "local.dev"
        documentroot: "/var/www/html"
      bar:
        servername: "local2.dev"
        documentroot: "/var/www/html"
      templated_site:
        template: tests/custom_template.conf.j2
        servername: "other.dev"
        somevariable: "somevalue"
    apache_vhosts_remove_sites:
      - baz
```
# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟