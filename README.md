## Deploy Rails Application

Using ansible to deploy rails application. Additionally you can switch to different user if you
don't have direct ssh access to the remote server.

## Requirements

ansible > 1.9

## Adding servers

Add hostnames inside inventory file under inventories path based on the environment.

## Deployment configuration

groups/all:

```
ssh_user: "{{ ssh_user }}"

home_path: "{{ ansible_env.HOME }}"

application_name: rails_app

# Branch to deploy
version: master

# Base directory where application resides
application_path: "{{ home_path }}/{{ application_name }}"

# Path where shared directory resides
shared_path: "{{ application_path }}/shared"

# Path where all the releases directory resides
releases_path: "{{ application_path }}/releases"

# Current release path
current_path: "{{ application_path }}/current"

git_repository_path: ''

# Environment variable to be set on the remote servers
env_variables:
  PATH: "{{ home_path }}/bin:/usr/bin:/bin"

config_files:
  - database.yml
  - redis.yml
  - secrets.yml
  - solr.yml
  - memcached.yml

# Minimum no. of releases to maintain
keep_releases: 5

```

Set common deployment configurations in group_vars/all file. Use other files under
group_vars for environment specific configurations.

## Starting deployment

```
ansible-playbook -i inventories/prod deploy.yml --extra-vars 'ssh_user=deploy'
```

**Note:** Use -K option to deploy other than ssh user.
