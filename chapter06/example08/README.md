# Instructions

Tested on:
- CentOS 7.6
- Ansible 2.7.5

To create the empty repository to be used for testing this playbook, you can run the following commands:
    mkdir /srv/app
    cd /srv/app
    git init
    git commit --allow-empty -m "initial commit"

Run this playbook using the command:

    ansible-playbook -i mastery-hosts error.yaml -v

To test the playbook actually deleting a branch, create the branch using the commands:

    cd /srv/app
    git branch badfeature
    cd -
    ansible-playbook -i mastery-hosts error.yaml -v
