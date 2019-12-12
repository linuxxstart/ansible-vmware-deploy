# ansible-vmware-deploy

Criação de vms no vCenter com o ansible.

# Pré requisitos
Matrix de compatibilidade dos sistemas operacionais das vms
http://partnerweb.vmware.com/programs/guestOS/guest-os-customization-matrix.pdf

Exemplo que estou usando é o ubuntu-18.04

Instalar o ansible

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

Instalar o pip do python para instalar a API de conexão com o vCenter.

```
sudo apt install python-pip
sudo pip install pyvmomi
```
# 1 Edita o arquivo com usuário e senha

Depois de clonar o repositório edite o arquivo.
```
sudo vim vcenter-vars.yml
```
Encripitar essas informções. Vai pedir para definir uma senha, pode ser qualquer uma, ela será pedida na exeção do playbook.
```
sudo ansible-vault encrypt vcenter-vars.yml
```

# 2 Edite infos que precisar no playbook

```
sudo vim /etc/ansible/playbooks/vcenter-task.yml
```

# 3 Executar  o playbook
```
sudo ansible-playbook -i vms_deploy vcenter-task.yml --ask-vault-pass -K
```
