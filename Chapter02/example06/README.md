# Instructions

Tested on:
- CentOS 7.6
- Ansible 2.7.5

Run the playbook as follows:

    ansible-playbook -i mastery-hosts inline.yaml

Then generate the encrypted variable to go inline as per the book:

    ansible-vault encrypt_string --vault-id test@./password.sh "secure_password" --name my_secret

Replace the variable definition in the playbook with the output of this command, then run the playbook again this time with the appropriate Vault ID to enable decryption:

    ansible-playbook -i mastery-hosts --vault-id test@./password.sh inline.yaml
