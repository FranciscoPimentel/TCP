# Projeto para subir o cluster Kubernetes versão 1.26.
# Será feito em Ansible/Phyton, para subir os servers Balanceadores, Control-Planes e workers, subirem de maneira horizontal.
# HaProxy com dois balanceadores, devido ao IP virtual.
Arquivo instalação TCP/haproxy.yml
Arquivo de Hosts: TCP/servers_haproxy
## Comandos úteis, recomendados na documentação, link: https://www.haproxy.com/documentation/hapee/latest/management/ansible/

ansible -i ./servers_haproxy loadbalancers -m ping
ansible -i ./servers_haproxy loadbalancers -u root -a "netstat -tlpn"
ansible -i ./servers_haproxy loadbalancers -u root -m shell -a "netstat -tlpn | grep :80"
ansible -i ./servers_haproxy loadbalancers -u root -m service -a "name=hapee-2.6-lb state=started" --check
ansible -i ./servers_haproxy loadbalancers -u root -m service -a "name=hapee-2.6-lb state=reloaded"