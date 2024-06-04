.. _setup:


Setting Up Snort on Ubuntu Using VMware
=======================================


This guide will walk you through the steps to set up Snort, an open-source network intrusion detection system, on an Ubuntu distribution running in a VMware virtual machine 

==================================
Step 1: Update and Upgrade Packages
===================================

Before installing Snort, make sure your system is up to date. Open a terminal and run the following commands:


 | ``$sudo apt-get update``
 

 | ``$sudo apt-get upgrade``
 
 
======================
Step 2: Install Snort
=======================

To install Snort, use the following command:


``$sudo apt-get install snort -y``

=============================
Step 3: Configure the Network
==============================


Next, we need to configure the network. Open a new terminal window and check your network interface configuration with:


``$ifconfig``

===============================
Step 4: Enable Promiscuous Mode
================================


To put the network interface in promiscuous mode, run:

``$sudo ip link set ens33 promisc on``


Replace ``ens33`` with your actual network interface name if it's different.

=======================================
Step 5: Install a Text Editor (Optional)
========================================

If you don't already have a text editor installed, you can install Vim with:


``$sudo apt-get install vim``

====================================
Step 6: Edit Snort Configuration File
======================================


Now, we need to edit the Snort configuration file. Open the configuration file using Vim:



``$sudo vim /etc/snort/snort.conf``


In the Snort configuration file, find the section for setting up network variables (Step 1) and replace the ``var HOME_NET any`` line with your actual IP address or network range. For example:


```var HOME_NET 192.168.1.0/24``

=======================
Step 7: Save and Exit
=======================

After making the necessary changes, save the file and exit Vim by pressing ``Esc``, typing ``:wq``, and pressing ``Enter``.

===============================
Step 8: Verify Snort Installation
===============================

To check if Snort is up and running, execute the following command:

``$snort -v``

You should see Snort start up and begin monitoring your network traffic.

Congratulations! You have successfully set up Snort on your Ubuntu system running in VMware.
