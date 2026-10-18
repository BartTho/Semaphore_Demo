## Repositories
- **name:** mijnRepo
- **Git URL:** https://github.com/BartTho/Semaphore_Demo.git
- **SSH Key:** /

## Key Store
- **name:** ansible
- **Type:** SSH Key
- **username:** ansible
- **Private Key:** -> copy inhoud van id_ed25519 -> cat .ssh/id_ed25519

## Variable Groups
### mijn_vars
**Extra:**
- ansible_python_interpreter     /usr/bin/python3
**Environment variables**

- ansible_connection    ssh
- ansible_user          ansible
- ansible_sudo_pass     Top.Secret
- ansible_become_exe    sudo.ws

