# ansible-vmware

Criação de vms no vCenter e cluster swarm com o ansible.

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
# 1 Criando variáveis

Depois de clonar o repositório edite o arquivo.
```
$ vim group_vars/all
```
Encripitar as senhas dos usuários everton@vsphere.local e root. Vai pedir para definir uma senha, pode ser qualquer uma, ela será pedida na exeção do playbook.
```
$ ansible-vault encrypt_string 'senhadoroot' --name 'qualquernome'
New Vault password: 
Confirm New Vault password: 
qualquernome: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          37303033376566363438653530306632393431346239396539613432663330326566633132666137
          6261353361386564363538343237386630333336633736630a343764623562653263343239636239
          63623537663735333430323233383535323438656130373534616335653831346464353539656461
          6337666564336538610a306131663636363933313630633661333432626430353264313866316266
          3665

Copiar a parte: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          37303033376566363438653530306632393431346239396539613432663330326566633132666137
          6261353361386564363538343237386630333336633736630a343764623562653263343239636239
          63623537663735333430323233383535323438656130373534616335653831346464353539656461
          6337666564336538610a306131663636363933313630633661333432626430353264313866316266
          3665
E cole na variavel de senha de root. Repita o processo com a senha do usuário everton@vsphere.local
```

# 2 Edite infos que precisar nos arquivos abaixo

```
$ vim vms_deploy
$ vim main.yml
$ vim roles/vms/tasks/main.yml
$ vim roles/manager/tasks/main.yml
$ vim roles/worker/tasks/main.yml
```

# 3 Executar  o playbook
```
$ ansible-playbook -i vms_deploy main.yml --ask-vault-pass
```
