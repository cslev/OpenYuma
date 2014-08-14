netconf
=======

Fork of the defacto standard Yuma project since it went proprietary.  Netconf is a management protocol (similar to SNMP) defined in RFC4741.

The original OpenYuma (https://github.com/OpenClovis/OpenYuma) version could only instantiate one netconf agent one PC.
This was caused by the fact that the netconf-subsystem communication was done via 
a generated socketfile (/tmp/ncxserver.sock) hardcoded in the source.

In order to alleviate this limitation, I modified the source.
Now, when --port argument is used/set a more unique socketfile will ge generated in /tmp
accordingly.

For instance, if you start a NETCONF agent with --port=830, then the socketfile will
be /tmp/ncx_server_830.sock.
After, you start another NETCONF agent with, say --port=832, then a new socketfile 
will be generated to provide a different communication 'channel'.

Note that the ports that you are going to use needs to be enabled in your sshd_config file, as it was in case of OpenClovis' version.

The install process is also the same as OpenClovis' version.
