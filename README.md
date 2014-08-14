netconf
=======

Fork of the defacto standard Yuma project since it went proprietary.  Netconf is a management protocol (similar to SNMP) defined in RFC4741.

The original OpenYuma (https://github.com/OpenClovis/OpenYuma) version could only instantiate one netconf agent on one machine/system.
This was caused by the fact that the netconf-subsystem communication was done via 
a generated socketfile (/tmp/ncxserver.sock) hardcoded in the source.

In order to alleviate this limitation, I modified the source.
Now, when --port argument is used/set a unique socketfile will be generated in /tmp 
directory accordingly.

For instance, if you start a NETCONF agent with --port=830, then the socketfile will
be /tmp/ncx_server_830.sock.
Later, when you start another NETCONF agent with, say --port=832, then a new socketfile 
will be generated to provide a different communication 'channel'.

Note that the ports that you are going to use needs to be enabled in your sshd_config file, as it was in case of OpenClovis' version.

In order to install this version of OpenYuma do the steps required for OpenClovis' version.


In Debian/Ubuntu based systems, install the following packages:
-------
 - libxml2-dev 
 - libssh2-1-dev 
 - libgcrypt11-dev 
 - libncurses5-dev 
 - make gcc automake 
 - openssh-client openssh-server ssh

Then, get the source:
-------
    git clone https://github.com/cslev/OpenYuma.git

    cd OpenYuma
    make
    sudo make install

In your sshd_config file, you need to add the ports that you want to use and tell
ssh server to use netconf-subsystem if connections from those ports are established.

Open sshd_config file for editing:
-------
    nano /etc/ssh/sshd_config

Add the following lines (under the assumption that you want to use port 830,831, and 832)
below the line Port 22:

    # ----- NETCONF -----
    Port 830
    Port 831
    Port 832
    Subsystem netconf /usr/sbin/netconf-subsystem
    # --- END NETCONF ---

Now, you are ready to use it via the following command using libtoaster as a module:   

    # netconfd --module=libtoaster --port=831




