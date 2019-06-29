# ossec

## How to start:

0. [OPTIONALY] Review config in `templates/server/ossec.conf` and `templates/agents/ossec.conf`
1. Add your `hosts` file with 2 groups [ossec_agents] and [ossec_server]
2. Execute command `ansible-playbook -i hosts ossec-server.yml`
3. Execute command `ansible-playbook -i hosts ossec-agents.yml --extra-vars "ossec_server= PLACE_IP_OF_OSSEC_SERVER"`
4. Prepare 2 terminal windows, you will need execute two plabybooks parallelly 
    1. In the first terminal execute `ansible-playbook -i hosts collecting-agents.yml`
    2. Wait for task: `TASK [Start ossec-authd (waiting 60s for communication from agents)]`
    3. Then execute in second terminal this line `ansible-playbook -i hosts add-agent.yml --extra-vars ossec_server= PLACE_IP_OF_OSSEC_SERVER`
    4. After your agents and ossec server should be started, and be ready to work.
    
## Disclaimers

1. Tested only on Ubuntu 18.04 LTS
2. Configs need to be adjusted after installation
    You should: 
    1. Adjust mailing information in /var/ossec/etc/ossec.conf on ossec-server host
    2. Change frequency of syschecks in /var/ossec/etc/ossec.conf on all hosts (you can adjust config before use this playbooks)
