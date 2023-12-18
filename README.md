# ansible
My collection of ansible playbooks for AWX

* use ubuntu hosts for remote execution
```shell
# From Docker Hub
docker pull arumugamsubramanian/ubuntu-ssh:main
# I use kind k8s cluster
docker run -d --network="kind" --name ubuntu-ssh -p 2222:22 arumugamsubramanian/ubuntu-ssh:main
```

#### Ansible Development Setup in Docker
* copy [env.example](env.example) to env
* Enter all the information in env
```shell
docker run --rm -it --network="kind" --env-file env \
  -v $(pwd):/app \
  --name ansible_servicenow_ee_dev \
  arumugamsubramanian/ansible-servicenow-ee:latest bash
  
cd /app
```
* Run ansible-playbook
```shell
# Execute the below commands under the folder
cd quick-demo
# to check only group
ansible ubuntu_ssh_kind_vpc -i dev_hosts.ini -m ping -u root --ask-pass
#to check all the hosts in inventory file
ansible all -i dev_hosts.ini -m ping -u root --ask-pass
# run playbook
ansible-playbook -i dev_hosts.ini 01-demo.yml -u root --ask-pass
# or add the password in inventory dev_hosts.ini
ansible-playbook -i dev_hosts.ini 01-demo.yml
```