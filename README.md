# Wazuh and Suricata Network Intrusion Detection Lab

## Project Overview

This project demonstrates how suspicious network traffic can be detected using Suricata IDS and monitored through the Wazuh security platform. The lab simulates a reconnaissance attack in the form of a port scan and shows how Suricata detects the activity and forwards alerts to Wazuh for visualization and analysis.

The goal of this lab is to understand how intrusion detection systems operate and how their alerts can be integrated into a SIEM platform for security monitoring.

## Objective

The objectives of this lab are:

* Understand the concept of suspicious network traffic
* Install and configure Suricata IDS
* Integrate Suricata alerts with Wazuh
* Simulate a network port scanning attack
* Visualize alerts in the Wazuh dashboard

## Suspicious Network Traffic

Suspicious network traffic refers to abnormal or unexpected activities observed on a network that may indicate malicious intent or the early stages of an attack.

Examples include:

* Port scanning activities performed by tools such as Nmap
* Connections to suspicious or unknown external IP addresses
* File transfers on uncommon ports
* Unusual HTTP or DNS traffic patterns

Detecting such activity is an important part of network monitoring and threat detection.

## Role of Intrusion Detection Systems

Intrusion Detection Systems monitor network traffic and identify potential threats by comparing observed traffic patterns against predefined detection rules.

Key functions of IDS include:

* Monitoring network traffic in real time
* Detecting known attack signatures
* Identifying reconnaissance activities
* Generating alerts for suspicious events
* Providing visibility to security teams

## About Suricata

Suricata is an open source network intrusion detection and prevention engine. It is widely used for network security monitoring due to its performance and extensive protocol analysis capabilities.

Important features of Suricata include:

* Deep packet inspection
* Multi-threaded processing
* Protocol identification (HTTP, TLS, DNS and others)
* JSON log output
* Integration with SIEM platforms such as Wazuh
* Community maintained detection rules

## Lab Environment

| Component        | Description                                       |
| ---------------- | ------------------------------------------------- |
| Wazuh Server     | Ubuntu server running Wazuh manager and dashboard |
| Wazuh Agent      | Ubuntu endpoint with Suricata installed           |
| Attacker Machine | Kali Linux used to simulate attacks               |

## Detection Scenario

In this lab a port scan is performed from the Kali Linux attacker machine. Suricata analyzes the incoming traffic and detects the scan using its rule set. The alert is written to the Suricata log file and collected by the Wazuh agent. Wazuh then processes the event and displays it in the dashboard.

Example attack command used during the test:

nmap -sS -T4 <target-ip>

The options used in this command are:

* sS : SYN scan
* T4 : faster scanning speed

This activity triggers Suricata rules related to network scanning.

## Viewing Alerts in Wazuh

After the attack simulation, alerts can be observed in the Wazuh dashboard.

Steps:

1. Log in to the Wazuh dashboard
2. Navigate to Security Events
3. Select the agent running Suricata
4. Filter events by Suricata

A typical alert generated during this lab is related to Nmap scanning activity.

## Learning Outcome

After completing this lab, the following concepts were understood:

* Basic operation of intrusion detection systems
* Installation and configuration of Suricata IDS
* Integration of Suricata logs with Wazuh
* Detection of port scanning attacks
* Visualization of network security alerts in a SIEM platform
