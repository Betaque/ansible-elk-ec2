
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
* You will need to add the kibana's domain name to nginx vars in main.yml. ```required```
```bash
  cd ansible-roles/nginx/vars
```
#### kibana dashboard
Kibana is a browser-based analytics and search dashboard for Elasticsearch. To see its interface, reverse proxy configurations are required which will handle by nginx role.

You need to map the dns with kibana installed machine IP. ```required```


## Command to deploy ELK components
```bash
  ansible-playbook provision.yml
```
## Configurations after installation

You need password of elastic user in logstash configuration file.

To get elastic password

* Connect with vm where elk installed

```
sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic
```
Copy the password from your terminal and paste in custom.conf in output plugin 
```
cd /etc/logstash/conf.d
vim custom.conf
  hosts => ["https://elastic:PASTE_HERE@localhost:9200"]

# Press i to insert in vi editor
# Press :wq to save 
```
Let's restart elasticsearch and logstash with
```
sudo systemctl restart logstash
sudo systemctl restart elasticsearch
```



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


