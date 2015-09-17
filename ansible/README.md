# InstallWLS_ansible

- Description:
Simple configuration to Install Weblogic and configure a Basic Domain

- Pre-Requirements:

jdk and wls.jar downloaded in a temp dir, in this example /opt/tmp, JAVA_HOME configured in /opt/java/latest linked to /opt/java/jdk_<version>.

Ansible installation: http://docs.ansible.com/ansible/intro_getting_started.html

- Config Structure:
/etc/ansible
          Run_WLS.yml
          hosts
          ansible.cfg
          roles/
              InstallWLS/
                      files/
                      tasks/
                          main.yml
                      template/
                          boot_properties.j2
                          create_domain_py.j2
                      vars/
                          main.yml
          groups_vars/
              appservers1
              appservers2

This configuration was made to do two installations of weblogic in 2 simulated machines (wlshost1 nad wlshots2) configured in /etc/hosts pointed to 127.0.0.1 with different ports to do working it.

One installation made in /opt/weblogic (wlshost1) and other in /usr/local/weblogic (wlshost2), those directorires must be created previously.

Finally to run the script, ansible-playbook needs to be executed: ansible-playbook Run_WLS.yml.

Run_WLS.yml: file of playbook to execute all config.
task/main.yml: all sequential tasks to be done
templates/boot_properties.j2: template to transfer to both weblogic servers in order to be started.
templates/create_domain_py.j2: py script to create a simple domain with a AdminServer.
vars/main.yml: common varibales for both machines and config
groups_var: specific varibales for groups of machines
host: inventory of machines grouped by type of service.
ansible.cfg: global configuration for ansible.

NOTE: response file and OraInventory for WebLogic instalation has been located into temp dir, in this case /opt/tmp/OraInv. This value is referenced in apprserversX group_vars.
