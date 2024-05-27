### Ansible Boilerplate to replicate into new project

```shell
docker run --rm -it --network="kind" --env-file ../env \
  -v $(pwd):/app \
  --name ansible_servicenow_ee_dev \
  arumugamsubramanian/ansible-servicenow-ee:latest bash
```

* this container has ansible user and sudo access to it for local development
```shell
# create a ssh home folder
ssh-keygen
# add remote machine keys to known_hosts
ssh-keyscan -H 172.18.0.7 >> ~/.ssh/known_hosts

cd /app

ansible all -m ping -i hosts
ansible all -m command -a "cat /etc/hosts" -i hosts
ansible all -a "cat /etc/hosts" -i hosts

# Run all tasks on all servers
ansible-playbook site.yml -v -i hosts

# Run all tasks only on group of servers
ansible-playbook anygroup.yml -v -i hosts

# Run all tasks only on individual server
ansible-playbook site.yml -v -l server1 -i hosts
```
