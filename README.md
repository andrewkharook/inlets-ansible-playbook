# Inlets ansible playbook

Ansible playbook to automatically set up the Inlets cloud tunnel to expose your internal and development endpoints to the public Internet via an exit-node. 
The script was inspired by the official inlets tutorial that can be found on [Alex Ellis' blog](https://blog.alexellis.io/https-inlets-local-endpoints/).

## Prerequisites
- you'll need an exit node. That could be a 5 USD VPS or any other computer with an IPv4 IP address. 
- sub-domain at duckdns.org. It's free and easy to set up.
- you'll need Ansible installed on your local computer. Take a look at [the docs](https://docs.ansible.com/ansible/latest/installation_guide/index.html) to find the installation guide for your OS.

## How to run
- rename the `vars.yml.example` to `vars.yml` and update config variables (see [Variables](#variables) section below).
- run the `server.yml` playbook to set up Inlets server on the exit node:

```
$ ansible-playbook server.yml
```

- run the `client.yml` playbook to set up Inlets client on the host node:

```
$ ansible-playbook client.yml
```

If asked for sudo password, add ` --ask-become-pass` parameter to the command.

### Variables
`pwd` - working direcotry on the exit node, e.g. `/home/foo`

`inlets_token` - your unique token. You can generate one by running `head -c 16 /dev/urandom | shasum | cut -d" " -f1`

`inlets_exit_node` - domain name or IP address of the exit node, e.g. `foobar.duckdns.org`

`inlets_host_node` - host name or IP address of the host node, e.g. `http://192.168.0.4:3000`

`duckdns_subdomain` - subdomain part of your duckdns domain that you've used for "inlets_exit_node", in this case `foobar`

`duckdns_api_key` - api key provided by duckdns.org for your subdomain

`ansible_exit_node` - name of the group in your ansible inventory file that contains exit node's IP address

`ansible_host_node` - name of the group in your ansoble inventory file that contains host node's IP address

