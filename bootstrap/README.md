# EDA Bootstrap

## Pre-Requisites
- ansible
- ansible.eda collection ```ansible-galaxy collection install ansible.eda```

## Export Required Environment Variables
```
export CONTROLLER_HOST="<https://eda.example.com>"
export CONTROLLER_USERNAME="admin"
export CONTROLLER_PASSWORD=$(kubectl get secret ansible-eda-admin-password -n eda -o jsonpath="{.data.password}" | base64 --decode ; echo)
```
## Update the playbook vars as needed
```
- name: Bootstrap EDA
  hosts: localhost
  gather_facts: false
  vars:
    aap_host: "<https://awx.example.com>"
    aap_token: "<AWX OAUTH TOKEN>"
    event_stream_token: "<RANDOM_BEARER_TOKEN_FOR_WEBHOOK_AUTH"
    event_stream_name: "<EVENT_STREAM_PREFIX>"
    git_repo: "<https://github.com/USER/RULEBOOK_REPO>"
    organization: Default
    decision_environment_image: "<quay.io/USER/DE_IMAGE>"
    decision_environment_name: "<DECISION_ENV_NAME>"
    project_name: "<PROJECT_NAME>"
```

## Run the Playbook from this folder
```
ansible-playbook playbooks/boostrap.yml
```