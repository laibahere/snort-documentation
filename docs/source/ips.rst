.. _idso:

What IDS/IPS is??
=================

Before delving into the installation and configuration of Snort, it's essential to understand the concepts of *Intrusion Detection Systems (IDS) and Intrusion Prevention Systems (IPS)*. These systems are crucial for maintaining network security by identifying and mitigating potential threats.

Intrusion Detection System (IDS)
--------------------------------

An IDS monitors network traffic for suspicious activity and issues alerts when such activity is detected. It does not block or reject the traffic but instead logs and alerts the system administrators for further action.

Types of IDS:
*************
1. **NIDS (Network Intrusion Detection System)**: Operates on the network level, monitoring traffic flow across the entire network.
   - **Working**: Sends alerts and logs traffic but does not drop or reject any traffic.

2. **HIDS (Host Intrusion Detection System)**: Monitors traffic from a single endpoint, such as a server or a computer.
   
   - **Working**: Alerts and logs but does not drop or reject traffic.

Intrusion Prevention System (IPS)
---------------------------------

An IPS goes a step further than IDS by actively blocking or rejecting malicious traffic in addition to alerting and logging.

Types of IPS:
*************

1. **NIPS (Network Intrusion Prevention System)**: Aims to protect the entire network.
   - **Working**: Sends alerts, logs network activity, and can also drop or reject malicious traffic.

2. **HIPS (Host Intrusion Prevention System)**: Protects a single endpoint by monitoring its traffic flow.
   - **Working**: Alerts, logs, and can drop or reject malicious traffic targeting the specific endpoint.

IDS and IPS Techniques
----------------------

Both IDS and IPS use three primary techniques to identify threats:
1. **Signature-Based**: Compares traffic against a database of known threat signatures. If a match is found, an alert is triggered.
2. **Behavior-Based**: Analyzes normal behavior patterns and flags anomalies. Unknown threats that do not match known signatures are identified based on abnormal behavior.
3. **Policy-Based**: Enforces predefined security policies to detect and prevent threats.

