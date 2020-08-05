# Ansible Role: Helm

Installs Helm on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
# Helm version number, specific Helm version format as 2.16.9
helm_version: latest

# Mirror to download Helm from
helm_mirror: "https://get.helm.sh"

# Dir where Helm should be installed
helm_install_dir: "/usr/local/bin"

# Directory to store files downloaded for Helm
helm_download_dir: "{{ x_ansible_download_dir | default(ansible_env.HOME + '/.ansible/tmp/downloads') }}"

helm_only_can_be_upgraded: false

helm_add_repos_for_current_user: true

helm_repos:
  - name: stable
    url: https://kubernetes-charts.storage.googleapis.com
```

if `helm_version` set `latest`, it will get latest version from github (https://github.com/helm/helm/releases/latest).

`helm_mirror` is the mirror to download helm from.

if `helm_install_dir` not on your `$PATH`, it will create `/usr/local/bin/helm` link to the helm real path.

if `helm_only_can_be_upgraded` set true, only new version of helm can be installed (override old one).

if `helm_add_repos_for_current_user` set true, helm repos defined in `helm_repos` will be added for current user.

users in china will be blocked to access default helm stable repo. We can use Azure helm repos as follow:
```
helm_repos:
  - name: stable
    url: https://mirror.azure.cn/kubernetes/charts/
  - name: incubator
    url: https://mirror.azure.cn/kubernetes/charts-incubator/
```

## Dependencies

None.

## Example Playbook

requirements.yml
```
- name: helm
  src: <repo_url>
  version: <branch_name>
  scm: git
```

playbook.yml
```
- hosts: servers
  roles:
    - helm
```
