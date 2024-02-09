
# ELK-Ansible

Ansible Playbook for setting up the ELK Stack on remote hosts


## Pre requisite

* Remote machine which allow to ssh
* Ansible installed on control node
* You need to map the dns with remote host IP where would elk install.


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
Copy the password from your terminal and paste in custom.conf in output plugin (store password safely)
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

## To access kibana dashboard

* Hit on the kibana domain that you mapped
* Choose option ```configure manually```
* Reset password for user kibana_system ```sudo /usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic```
* Get verification code by running ```systemctl status kibana```
* Paste the output in password, tick on checkbox and click on ```configure elastic```
* It will prompt for elastic user login creds, put and login



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


