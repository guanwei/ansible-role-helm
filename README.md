# Ansible Role: Helm

Installs Helm on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
# specific helm version format as v2.16.9
helm_version: latest
helm_add_repos_for_current_user: true
helm_only_can_be_upgraded: false
helm_repos:
  - name: stable
    url: https://kubernetes-charts.storage.googleapis.com
```

if `helm_version` set latest, it will get latest version from github (https://github.com/helm/helm/releases/latest).

if `helm_add_repos_for_current_user` set true, helm repos defined in `helm_repos` will be added for current user.

if `helm_only_can_be_upgraded` set true, only new version of helm can be installed (override old one).

## Dependencies

None.

## Example Playbook

requirements.yml
```
- name: helm
  src: ssh://tfsemea1.ta.philips.com:22/tfs/TPC_Region27/CDI_PT/_git/ansible-role-helm
  version: dev
  scm: git
```

playbook.yml
```
- hosts: servers
  roles:
    - helm
```
