Snort Usage Guide
=================


Snort is a powerful open-source network intrusion detection system (NIDS) that can perform real-time traffic analysis and packet logging. This guide will help you understand how to use Snort effectively, including testing your configuration, logging data, filtering logs, and making the logs human-readable.


Basic Snort Commands
********************


Checking the Configuration File
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


To verify that your Snort configuration file is running successfully, use the following command:


.. code-block:: shell

    sudo snort -c /etc/snort/snort.conf -T


- `-c`: Specifies the configuration file.

- `-T`: Runs Snort in self-test mode to check the configuration file.


Viewing Snort Version
~~~~~~~~~~~~~~~~~~~~~


To view the version of Snort you are using:


.. code-block:: shell

    snort -V


Running Snort in Different Modes
********************************


Verbose Mode
~~~~~~~~~~~~


To run Snort in verbose mode:


.. code-block:: shell

    snort -v


- `-v`: Displays packet data.


Verbose Mode with Detailed Information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


To run Snort in verbose mode with packet and data link layer information:


.. code-block:: shell

    snort -vd


Verbose Mode with Detailed Information and Payload
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


To include application layer payload information:


.. code-block:: shell

    snort -v -d -e


Hex Dump Mode
~~~~~~~~~~~~~


To run Snort and display the payload in hexadecimal:


.. code-block:: shell

    snort -X


Logging Data
************


Logging to a Directory
~~~~~~~~~~~~~~~~~~~~~~


To log Snort data to a directory:


.. code-block:: shell

    sudo snort -X -l .


- `-X`: Hexadecimal and ASCII data dump of the packet payload.

- `-l .`: Logs data to the current directory.


Reading and Viewing Logs
~~~~~~~~~~~~~~~~~~~~~~~~


To read the logged data:


.. code-block:: shell

    sudo snort -r snort.log.{file}


- `-r`: Read and process a log file.


Filtering Logs by Port
~~~~~~~~~~~~~~~~~~~~~~


To filter the log data by a specific port (e.g., HTTP traffic on port 80):


.. code-block:: shell

    sudo snort -r snort.log.{file} 'port 80'


Making Logs Human-Readable
~~~~~~~~~~~~~~~~~~~~~~~~~~


To convert logs into a human-readable form:


.. code-block:: shell

    sudo snort -dev -K ASCII -l .


- `-d`: Display the application layer data.

- `-e`: Display the link layer header information.

- `-v`: Verbose mode.

- `-K ASCII`: Output logs in ASCII format.


Removing Log Files
~~~~~~~~~~~~~~~~~~


To remove a specific log file:


.. code-block:: shell

    sudo rm -r snort.log.{file}


Running Snort as an IDS
~~~~~~~~~~~~~~~~~~~~~~~


To run Snort as an intrusion detection system (IDS) and log alerts in full detail:


.. code-block:: shell

    sudo snort -c /etc/snort/snort.conf -A full -l . -r mx-1.pcap


- `-A full`: Full alert mode, displaying detailed alert information.

- `-r mx-1.pcap`: Reads packets from the specified pcap file.


Snort Alert Modes
*****************


Snort supports different alert modes, including:


- **Console mode**: Only the payload header is printed.

- **Fast mode**: Shows the alert message, timestamp, source and destination IP, along with port numbers.

- **CMG mode**: Basic header details with payload in hex and text format.

- **None**: Disables alerting.


To run Snort with a specific alert mode:


.. code-block:: shell

    sudo snort -c /etc/snort/snort.conf -A {mode} -l .


Replace `{mode}` with `full`, `fast`, `console`, `cmg`, or `none` as needed.


Example Commands
****************


Example 1: Full Details from PCAP
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. code-block:: shell

    sudo snort -c /etc/snort/snort.conf -A full -l . -r mx-1.pcap


Example 2: Different Configuration File
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. code-block:: shell

    sudo snort -c /etc/snort/snortv2.conf -A full -l . -r mx-1.pcap


By following these commands and guidelines, you can effectively use Snort to monitor and analyze network traffic, ensuring your network's security and integrity. For more detailed information, refer to the `Snort documentation <https://www.snort.org/documentation>`_.

