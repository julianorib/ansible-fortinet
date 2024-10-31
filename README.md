# Ansible WSL

## Reference: 
<https://community.fortinet.com/t5/FortiGate/Technical-Tip-Application-of-Ansible-on-FortiGate/ta-p/258346>\
<https://docs.ansible.com/ansible/latest/collections/fortinet/fortios/index.html>\
<https://www.youtube.com/watch?v=RzUlruC2CA4>

## Install ansible 
```
sudo apt install ansible
```

## Criar projeto teste
```
mkdir fortigate && cd fortigate
```

## Instalar collection Fortios.
ansible-galaxy collection install fortinet.fortios


## Criar arquivo de inventário.
```
touch hosts.cfg
```
```
[firewall]
fortigate1 ansible_host=10.1.1.1 ansible_user="admin" ansible_password="password"

[firewall:vars]
ansible_network_os=fortinet.fortios.fortios
```

## Criar um playbook de exemplo

```
hosts: firewall
tasks:
- name: Change hostname
  fortinet.fortios.fortios_system_global:
    system_global:
      hostname: “FortiGate_Lab”

- name: Create Address
  fortinet.fortios.fortios_firewall_address:
    state: “present”
    firewall_address:
      name: test_123
      subnet: 10.1.1.1 255.255.255.0
```

## Aplicar o playbook.
```
ansible-playbook -i hosts.cfg playbook.yaml
```