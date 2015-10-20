## Deploy Rails Application

Using ansible to deploy rails application. Additionally you can switch to different user if you
don't have direct ssh access to the remote server.

## Requirements

ansible > 1.9

## Adding servers

Add hostnames inside inventory file under inventories path based on the environment.

## Deployment configuration

Set common deployment configurations in group_vars/all file. Use other files under
group_vars for environment specific configurations.

## Starting deployment

ansible-playbook -i inventories/prod deploy.yml --extra-vars 'ssh_user=deploy'

**Note:** Use -K option to deploy other than ssh user.
