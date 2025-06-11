# Ansible Role "fredericpetit-gh.graylog-minimal-conf-containerized"

[🇲🇫] Rôle Ansible pour déployer une configuration minimale pour Graylog avec MongoDB et OpenSearch, en conteneurs. - [🇬🇧] Ansible role to deploy minimal configuration for Graylog with MongoDB and OpenSearch, containerized.

**WORKS WITH DOCKER & PODMAN !**

## Description

This role configure this containers :
- Graylog 6 (exposed on port 9000)

## Default Variables

| Variable                    | Description               | Default Value                                     |
|-----------------------------|---------------------------|---------------------------------------------------|
| `mongo_image`               | Image Docker MongoDB      | `mongo:6-jammy`                                   |
| `opensearch_image`          | Image Docker OpenSearch   | `opensearchproject/opensearch:1`                  |
| `graylog_image`             | Image Docker Graylog      | `graylog/graylog:6`                               |
| `mongo_container_name`      | Container name MongoDB    | `ubuntu-mongo`                                    |
| `opensearch_container_name` | Container name OpenSearch | `amazon-opensearch`                               |
| `graylog_container_name`    | Container name Graylog    | `ubuntu-graylog`                                  |
| `graylog_admin_password`    | Password Graylog          | `root`                                            |
| `graylog_password_secret`   | Secret key Graylog        | `root`                                            |
| `graylog_http_external_uri` | URL Graylog               | `http://{{ ansible_default_ipv4.address }}:9000/` |
| `graylog_api_auth_token`    | Token                     | empty                                             |
| `graylog_input_name`        | Input name                | `Test01`                                          |
| `graylog_input_type`        | Input type                | `org.graylog2.inputs.gelf.udp.GELFUDPInput`       |
| `graylog_input_port`        | Input port                | `12201`                                           |

## Requirements

This role requires :
- Docker OR Podman installed on the target host.
- The Ansible collection `community.docker` installed locally (`ansible-galaxy collection install community.docker`) for Docker OR `containers.podman`(`ansible-galaxy collection install containers.podman`) for Podman.

## Installation

To add in the requirements.yaml file :

```yaml
- src: fredericpetit-gh.graylog-minimal-conf-containerized
  version: 1.0.0
```

OR

```yaml
- src: git+https://gitlab.com/fredericpetit/ansible-role-graylog-minimal-conf-containerized.git
  name: graylog-minimal-conf-containerized
  version: main
```

Then run : `ansible-galaxy role install -r requirements.yaml --force`

## Usage

Add the role in a playbook, like this for example :

```yaml
- name: Configure Graylog with MongoDB and OpenSearch (containers)
  hosts: docker
  become: yes
  gather_facts: true

  roles:
    - fredericpetit-gh.graylog-minimal-conf-containerized
```

Then run : `ansible-playbook -i inventory playbooks/graylog/conf.yaml`