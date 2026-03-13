# Suricata Installation and Configuration

This document describes the steps used to install and configure Suricata IDS on an Ubuntu system and integrate it with Wazuh.

## Installing Suricata

Add the Suricata repository:

 * sudo add-apt-repository ppa:oisf/suricata-stable

Update the package list:

 * sudo apt-get update

Install Suricata:

 * sudo apt-get install suricata -y

## Downloading Detection Rules

Download the Emerging Threats rule set:

 * cd /tmp
 * curl -LO https://rules.emergingthreats.net/open/suricata-6.0.8/emerging.rules.tar.gz

Extract the rules:

 * sudo tar -xvzf emerging.rules.tar.gz

Create the rules directory if it does not exist:

 * sudo mkdir /etc/suricata/rules

Move the rules to the Suricata rules directory:

 * sudo mv rules/*.rules /etc/suricata/rules/

Set appropriate permissions for the rule files:

 * sudo chmod 640 /etc/suricata/rules/*.rules

## Restarting Suricata

Restart the Suricata service:

 * sudo systemctl restart suricata

Verify that the service is running:

 * sudo systemctl status suricata

## Verifying Suricata Logs

Suricata stores alerts in the JSON log file:

 * /var/log/suricata/eve.json

To monitor the alerts in real time:

 * sudo tail -f /var/log/suricata/eve.json

## Integrating Suricata with Wazuh

To allow the Wazuh agent to collect Suricata alerts, edit the Wazuh agent configuration file:

 * sudo nano /var/ossec/etc/ossec.conf

Add the following configuration block:

 * <localfile>
    <log_format>json</log_format>
    <location>/var/log/suricata/eve.json</location>
  </localfile>

Restart the Wazuh agent to apply the configuration:

 * sudo systemctl restart wazuh-agent

After this configuration, Suricata alerts will be collected by Wazuh and displayed in the dashboard.


