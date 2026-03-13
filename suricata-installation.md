\# Suricata Installation and Configuration



This document describes the steps used to install and configure Suricata IDS on an Ubuntu system and integrate it with Wazuh.



\## Installing Suricata



Add the Suricata repository:



&nbsp;\*sudo add-apt-repository ppa:oisf/suricata-stable



Update the package list:



&nbsp;\*sudo apt-get update



Install Suricata:



&nbsp;\*sudo apt-get install suricata -y



\## Downloading Detection Rules



Download the Emerging Threats rule set:



&nbsp;\*cd /tmp

&nbsp;\*curl -LO https://rules.emergingthreats.net/open/suricata-6.0.8/emerging.rules.tar.gz



Extract the rules:



&nbsp;\*sudo tar -xvzf emerging.rules.tar.gz



Create the rules directory if it does not exist:



&nbsp;\*sudo mkdir /etc/suricata/rules



Move the rules to the Suricata rules directory:



&nbsp;\*sudo mv rules/\*.rules /etc/suricata/rules/



Set appropriate permissions for the rule files:



&nbsp;\*sudo chmod 640 /etc/suricata/rules/\*.rules



\## Restarting Suricata



Restart the Suricata service:



&nbsp;\*sudo systemctl restart suricata



Verify that the service is running:



&nbsp;\*sudo systemctl status suricata



\## Verifying Suricata Logs



Suricata stores alerts in the JSON log file:



&nbsp;\*/var/log/suricata/eve.json



To monitor the alerts in real time:



&nbsp;\*sudo tail -f /var/log/suricata/eve.json



\## Integrating Suricata with Wazuh



To allow the Wazuh agent to collect Suricata alerts, edit the Wazuh agent configuration file:



&nbsp;\*sudo nano /var/ossec/etc/ossec.conf



Add the following configuration block:



&nbsp;\*<localfile>

&nbsp;   <log\_format>json</log\_format>

&nbsp;   <location>/var/log/suricata/eve.json</location>

&nbsp; </localfile>



Restart the Wazuh agent to apply the configuration:



&nbsp;\*sudo systemctl restart wazuh-agent



After this configuration, Suricata alerts will be collected by Wazuh and displayed in the dashboard.



