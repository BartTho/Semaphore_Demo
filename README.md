# Installatie Semaphore  
```
services:
  mysql:
    restart: unless-stopped
    image: mysql:8.0
    hostname: mysql
    volumes:
      - semaphore-mysql:/var/lib/mysql
    environment:
      MYSQL_RANDOM_ROOT_PASSWORD: 'yes'
      MYSQL_DATABASE: semaphore
      MYSQL_USER: semaphore
      MYSQL_PASSWORD: semaphore
  semaphore:
    restart: unless-stopped
    ports:
      - 3333:3000
    image: semaphoreui/semaphore:latest
    environment:
      SEMAPHORE_DB_USER: semaphore
      SEMAPHORE_DB_PASS: semaphore
      SEMAPHORE_DB_HOST: mysql # for postgres, change to: postgres
      SEMAPHORE_DB_PORT: 3306 # change to 5432 for postgres
      SEMAPHORE_DB_DIALECT: mysql # for postgres, change to: postgres
      SEMAPHORE_DB: semaphore
      SEMAPHORE_PLAYBOOK_PATH: /tmp/semaphore/
      SEMAPHORE_ADMIN_PASSWORD: Top.Secret
      SEMAPHORE_ADMIN_NAME: admin
      SEMAPHORE_ADMIN_EMAIL: admin@localhost
      SEMAPHORE_ADMIN: admin
      SEMAPHORE_ACCESS_KEY_ENCRYPTION: 6vdTsSIahpP/HT8tkm/h/aRy/ABdfA4K8cusae0EtnA=
      SEMAPHORE_LDAP_ACTIVATED: 'no'
      TZ: UTC
    depends_on:
      - mysql # for postgres, change to: postgres
volumes:
  semaphore-mysql: # to use postgres, switch to: semaphore-postgres
```

# Configuratie Semaphore
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
