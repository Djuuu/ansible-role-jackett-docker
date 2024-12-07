Ansible Role: Jackett-docker
============================

Install Jackett Docker Compose project.

- https://github.com/Jackett/Jackett

Based on LinuxServer.io image: https://docs.linuxserver.io/images/docker-jackett/

Requirements
------------

Requires the following to be installed:
- docker
- docker compose

Role Variables
--------------

Common system variables:

```yaml
timezone: UTC
```

Common Docker projects variables:

```yaml
# Base directory for Docker projects
docker_projects_path: # /var/apps
```

Available role variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker project variables

jackett_project_name: jackett

# Docker project dynamic vars (uses `docker_project_name` prefix, adapt if overriden)

# Port targeted by Traefik router
jackett_traefik_loadbalancer_server_port: 9117
jackett_traefik_middlewares:
  - "internal-access@file"

# Flaresolverr service additional docker-compose options (ex: cpu_shares, deploy, ...)
jackett_flaresolverr_compose_service_additional_options: ""


# Jackett project variables

# lscr.io/linuxserver/jackett image version
jackett_version: latest

# ghcr.io/flaresolverr/flaresolverr image version
jackett_flaresolverr_version: latest

# Jackett blackhole directory
jackett_download_dir: "{{ docker_project_path }}/downloads"
```

Dependencies
------------

This role depends on :
- [djuuu.docker_project](https://github.com/Djuuu/ansible-role-docker-project)

Some variables allow integration with:
- [djuuu.traefik_docker](https://github.com/Djuuu/ansible-role-traefik-docker)

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: true
  gather_subset:
    - "!all"
    - "!min"
    - user_id

  roles:
    - djuuu.jackett_docker
```

License
-------

Beerware License
