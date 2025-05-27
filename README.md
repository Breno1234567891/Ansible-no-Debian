# Ansible-no-Debian
# Instalação do Ansible no Debian

Este repositório documenta o processo detalhado de instalação e primeiros passos com o **Ansible** em sistemas Debian (como Debian 10, 11 ou 12).

---

## Requisitos

- Sistema operacional: **Debian**
- Permissões de **superusuário**
- Conexão com a internet

---

## 1. Atualizar o Sistema

```bash
sudo apt update && sudo apt upgrade -y
```

## 2. Instalar o Ansible
```bash
sudo apt install ansible -y
```
Verifique se foi instalado corretamente:
```bash
ansible --version
```

## 3. Criar Inventário de Hosts
Crie o arquivo hosts.ini:
```bash
[servidores]
192.168.1.100 ansible_user=debian

[servidores:vars]
ansible_python_interpreter=/usr/bin/python3
```

Substitua 192.168.1.100 pelo IP real da sua máquina remota.

## 4. Testar Conexão
Certifique-se de que o host remoto aceita conexões SSH da máquina local.

Teste a conexão com o módulo ping:

```bash
ansible -i hosts.ini servidores -m ping
````

## 5. Criar um Playbook de Exemplo
Arquivo: atualizar.yml
```bash
---
- name: Atualizar pacotes em máquinas Debian
  hosts: servidores
  become: yes

  tasks:
    - name: Atualizar cache de pacotes
      apt:
        update_cache: yes

    - name: Atualizar todos os pacotes
      apt:
        upgrade: dist
```

Execute o playbook:
```bash
ansible-playbook -i hosts.ini atualizar.yml
```




