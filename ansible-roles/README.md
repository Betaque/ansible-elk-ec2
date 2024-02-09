
# ELK-Ansible

Ansible Playbook for setting up the ELK Stack on remote hosts


## Pre requisite

* Remote machine which allow to ssh
* Ansible installed on control node


## Command to use this project



```bash
  git clone <url>
  cd elk-ansible
```

## Configurations before installation
* To configure this project, values are passed through vars directory of every role. ```optional```

* You will need to add the host's IP to hosts file. ```required```
```bash
  cd hosts
```

## Command to deploy ELK components
```bash
  ansible-playbook provision.yml
```
## Access kibana dashboard
Kibana is a browser-based analytics and search dashboard for Elasticsearch. To see its interface, reverse proxy configurations are required which will handle by nginx role.

You need to map the dns with kibana installed machine IP. ```required```


## File hierarchy

```
ansible
├── elasticsearch
│   ├── tasks
│   │   └── main.yml
│   └── vars
│       └── main.yml
├── kibana
│   ├── tasks
│   │   └── main.yml
│   └── vars
│       └── main.yml
├── logstash
│   ├── tasks
│   │   └── main.yml
│   └── vars
│       └── main.yml
├── nginx
│   ├── tasks
│   │   └── main.yml
│   └── vars
│       └── main.yml
├── README.md
├── ansible.cfg
├── hosts
└── provision.yaml
```


