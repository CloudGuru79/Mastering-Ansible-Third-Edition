# Instructions

Tested on:
- CentOS 7.6
- Ansible 2.7.5

Create a password script for your new Vault called `password.sh` that contains:

    #!/bin/sh
    echo "a long password"

Remember to make the script executable:

    chmod +x password.sh

Then run this command to create the vault:

    ansible-vault create --vault-id ./password.sh even_more_secrets.yaml

Try editing it and manually entering the password from the script above using the command:

    ansible-vault edit --vault-id @prompt even_more_secrets.yaml

Later try re-keying this with the command:

    ansible-vault rekey --vault-id password.sh --new-vault-id dev@./password_file even_more_secrets.yaml

