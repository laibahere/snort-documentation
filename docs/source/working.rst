**Running Snort and Managing Configuration**
========================================

*To understand Snort commands, use the manual:*
--------------------------------------------

``$ man snort``

This will give an overview of how Snort commands operate.


Testing the Configuration File
-------------------------------
To test your Snort configuration file:


``$ sudo snort -T -i ens33 -c /etc/snort/snort.conf``


* `-T`: Tests the configuration and exits.
* `-i ens33`: Specifies the network interface to monitor.
* `-c /etc/snort/snort.conf`: Specifies the configuration file to use.


Managing Snort Rules
--------------------

If there are too many incoming packets and the output is hard to read, you can comment out custom rules. 


1. **Set up Vim for easier navigation:**


   Open your Vim configuration file:
   
   
   ``$ sudo vim /root/.vimrc``
   
   Add the following lines to enable line numbers and syntax highlighting:
   
   
         | set number 
         | syntax on.
      
      
2. **Comment out custom rules in the Snort configuration:**
   Open the Snort configuration file:
   
   
   ``$ sudo vim /etc/snort/snort.conf``
   
   Scroll down to the section with custom rules (starting at line 598 and ending at line 717). Use Vim’s colon functionality to comment out these lines:
   
   
   1. Press `Esc` to ensure you're in normal mode.
   2. Type `:598,717s/^/#` and press `Enter`.

3. **Leave local rule specifications unchanged.**

Running Snort with Updated Configuration
----------------------------------------

Run the Snort command again:


``$ sudo snort -T -i ens33 -c /etc/snort/snort.conf``


Now, the only rules loaded will be those within the `local.rules` file, reducing the clutter in the output.
