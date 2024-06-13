.. _remem:


To Remember:
============


Snort is a widely-used open-source network intrusion detection system (NIDS) and intrusion prevention system (IPS).


This documentation provides detailed guidance on configuring Snort, including setting up key configuration files, defining network variables, selecting data acquisition modules (DAQ), and managing logging, alerting, and rules.


Configuration Files
-------------------


Two primary configuration files are used in Snort:


- **snort.conf**: This is the main configuration file where most of Snort's settings are specified.

- **local.rules**: This file is used for user-generated rules, allowing customization of Snort's detection capabilities.


Network Variable Definitions
----------------------------


Network variables in Snort define the internal and external networks that Snort monitors and protects. These variables are crucial for creating effective detection rules.


HOME_NET
~~~~~~~~


- **Description**: Represents the network or networks you are protecting.

- **Example**: 

  - To protect any network: ``any``

  - To protect a specific subnet: ``192.168.1.1/24``


EXTERNAL_NET
~~~~~~~~~~~~


- **Description**: Represents the external network, usually everything outside of the HOME_NET. It can be set to any network or exclude the HOME_NET.

- **Example**: 

  - Any external network: ``any``

  - Exclude the HOME_NET: ``!$HOME_NET``

RULE_PATH
~~~~~~~~~

- **Description**: The directory path where Snort's rules are stored.

- **Example**: ``/etc/snort/rules``


SO_RULE_PATH
~~~~~~~~~~~~


- **Description**: Path for shared object rules, which are precompiled rules provided by Snort.


- **Example**: ``$RULE_PATH/so_rules``


PREPROC_RULE_PATH
~~~~~~~~~~~~~~~~~


- **Description**: Path for preprocessor rules, which are additional rules used by Snort preprocessors.

- **Example**: ``$RULE_PATH/plugin_rules``


IPS Mode Configuration
----------------------


Snort can operate in different modes depending on the selected Data Acquisition Module (DAQ). DAQ modules allow Snort to interface with network packets in various ways.


Data Acquisition Modules (DAQ)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Here are the different DAQ modules Snort supports:

- **Pcap**: The default mode, also known as Sniffer mode. It captures packets for analysis.

- **Afpacket**: Used for inline mode, which enables IPS capabilities.

- **Ipq**: Inline mode for Linux, utilizing Netfilter. It replaces the older snort_inline patch.

- **Nfq**: Another inline mode for Linux, also using Netfilter.

- **Ipfw**: Inline mode for OpenBSD and FreeBSD using divert sockets, and compatible with pf and ipfw firewalls.

- **Dump**: A testing mode for both inline and normalization.


The most commonly used modes are pcap for simple packet capture and afpacket for inline IPS functionality.


Step-by-Step Configuration for IPS Mode
---------------------------------------


To configure Snort in IPS mode, follow these steps:


1. **Select the DAQ Module**:
   

   Specify the DAQ module to use:

   
   .. code-block:: shell
   
      config daq: afpacket

     
2. **Activate Inline Mode**:


   Set the mode to inline:


   .. code-block:: shell
   
      config daq_mode: inline



3. **Set the Log Directory**:


   Define the directory for logs:

   
   .. code-block:: shell
   
      config logdir: /var/logs/snort


Output Plugins Configuration
----------------------------


Snort supports various output plugins for logging and alerting, allowing flexible management of detection outputs. By default, Snort logs everything to the console, but this can be configured to log to files, databases, or other systems for more efficient management.


Example Configuration
~~~~~~~~~~~~~~~~~~~~~


To log alerts to a file, you can configure Snort as follows:


.. code-block:: shell

   output alert_fast: alert.ids


Customizing the Ruleset
-----------------------


Including Custom and Default Rules


To effectively use Snort, you need to manage the rulesets by including necessary rule files in the configuration.


1. **Include Local Rules**:


   Add your custom rules:
   

   .. code-block:: shell
   
      include $RULE_PATH/local.rules
     

2. **Include Default or Downloaded Rules**:


   Add default or community-provided rules:
   

   .. code-block:: shell
   
      include $RULE_PATH/community.rules


**Note**: Lines starting with `#` are comments. Remove the `#` to activate a configuration line.

