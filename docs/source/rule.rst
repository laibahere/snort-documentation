Understanding Snort Rules
=========================


Snort rules are critical for identifying and mitigating network threats. 


It’s important to properly write Snort rules so they work as intended; that is, so that they successfully identify emerging threats within your network. To do this, you need a clear grasp of Snort syntax and how the rules are formed.


While Snort rules are usually written in a single line, recent versions of Snort allow for multi-line rules; this is especially useful for more sophisticated rules that can be difficult to restrict to just one line.


They consist of two main parts:

1. **the rule header**

2. **rule options**


Understanding and properly writing these rules ensures effective network monitoring and threat detection.


Rule Header
~~~~~~~~~~


The rule header contains network-based information:

- **Action**:

 Specifies what action to take when traffic matches the rule. Common actions include ``alert`` (generate an alert), ``log`` (log the packet), and ``pass`` (ignore the packet).


- **Protocol**:

 The protocol to inspect (e.g., ``tcp``, ``udp``, ``icmp``).


- **Source IP Address**:

 The IP address of the traffic source. Variables like ``$HOME_NET`` (internal network) and ``$EXTERNAL_NET`` (external network) are often used.


- **Source Port**: 

The port number of the source. ``any`` can be used to specify all ports.



- **Direction**:

 Indicates the direction of traffic. ``->`` denotes traffic from source to destination, while ``<->`` indicates bidirectional 
 traffic.
 
 
- **Destination IP Address**: 

The IP address of the traffic destination.


- **Destination Port**: 

The port number of the destination.


Example:
~~~~~~~~


.. code-block:: shell

    alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS


This rule will generate an alert for any TCP traffic from the internal network to external networks on HTTP ports.


Rule Options
------------


The rule options provide detailed criteria for packet inspection:


- **Message (`msg`)**: 

 Describes the rule’s purpose. This message is displayed when the rule triggers.


- **Flow (`flow`)**: 

Defines the flow of the traffic. Common options include ``to_server``, ``to_client``, ``established``, etc.


- **Content (`content`)**:

 Specifies the data or pattern to look for within the packet payload.

- **Service/Application Protocol**: 

Indicates the application-layer protocol to match (e.g., HTTP, FTP).


- **Snort ID (`sid`)** and **Revision number (`rev`)**: 

Unique identifiers for the rule and its version. ``sid`` is a unique rule ID, and ``rev`` denotes the version of the rule.


Example Snort Rules
~~~~~~~~~~~~~~~~~~~


1. **Detecting a DoS Attack using Docker Honeypots**


   .. code-block:: shell

      alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"DoS attack detected from Docker honeypot"; flow:established,to_server; content:"GET"; http_uri; sid:1000001; rev:1;)


   This rule generates an alert for any established TCP connection from the internal network to external networks on HTTP ports where the packet contains the string "GET" in the URI, indicative of a potential DoS attack from a compromised Docker honeypot.


2. **Detecting SSH Login Attempts**


   .. code-block:: shell

      alert tcp $EXTERNAL_NET any -> $HOME_NET 22 (msg:"SSH login attempt"; flow:established,to_server; content:"SSH"; sid:1000002; rev:1;)


   This rule triggers an alert for any established TCP connection from external networks to the internal network on port 22 (SSH) containing the string "SSH", which could indicate an SSH login attempt.

Writing Effective Snort Rules
-----------------------------


To write effective Snort rules:


- **Understand the threat**: Know what you are trying to detect.

- **Use clear and specific patterns**: Ensure content and flow options precisely define the traffic to match.

- **Keep rules updated**: Regularly revise rules to adapt to new threats.

- **Test rules**: Verify that rules work as intended without causing false positives.


Implementing Snort in your cybersecurity stack provides a flexible and platform-agnostic approach to securing your network against known and emerging network security threats. However, the rules must be configured to work properly.


While you could write your own Snort rules for fairly straightforward use cases, keeping the rules up to date with emerging threats is a challenging task. Instead, consider using Snort and YARA rules created by experts, like the freely available Community ruleset.

There is a web-based Snort rule creator :ref:`snorpy <snocp>`
