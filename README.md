## Repositories
- **name:** -> mijnRepo
- **Git URL:** -> https://github.com/BartTho/Semaphore_Demo.git
- **SSH Key:** -> /

## Key Store.   
- **name:** -> ansible   
- **Type:** -> SSH Key    
- **username:** -> ansible     
- **Private Key:** -> copy inhoud van id_ed25519 -> cat .ssh/id_ed25519   

## Variable Groups    
### mijn_vars    
**Extra:**.   
- ansible_python_interpreter -> /usr/bin/python3   

**Environment variables**.     
- ansible_connection    -> ssh   
- ansible_user          -> ansible   
- ansible_sudo_pass     -> Top.Secret   
- ansible_become_exe    -> sudo.ws     

## Inventory
**mijnIventory**
- **Name:** -> mijnIventory
- **User Credentials:** -> ansible
- **Sudo Credentials (Optional):** -> /
- **Type:** -> Static
#### Voorbeeld.   
[ubuntu26]   
192.168.157.145   
192.168.157.147   
    
[rocky]   
192.168.157.146  
   
[ubuntu26:vars]   
ansible_become_exe=sudo.ws   

## Task Template
**Name:** -> mijndemo1
**Path to playbook file:** -> playbook.yaml
**Inventory:** -> mijnIventory
**Repository:** -> mijnRepo
**Branch / Tag:** -> main
**Variable Group:** -> mijn_vars
**View:** -> All


## Task Template
**Name:** -> mijndemo2
**Path to playbook file:** -> playbook2.yaml
**Inventory:** -> mijnIventory
**Repository:** -> mijnRepo
**Branch / Tag:** -> main
**Variable Group:** -> mijn_vars
**View:** -> All
