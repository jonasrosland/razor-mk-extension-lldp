Razor MicroKernel Extension to identify Server Locality using LLDP
========

### What does it do?

From the node that is booted with the MicroKernel, it asks for information about the switch it's connected to such as the name of the switch, switch port, switch IP and other information that is available using regular LLDP, a standardized version of CDP, which can be used on pretty much any standard datacenter switch today (just make sure it's enabled).

### What for?

With this MicroKernel extension together with a simple and proper LLDP configuration on your switches, we can easily define what Razor policy should be applied to a specific server based on server locality within a rack and/or datacenter. One example (thanks @mcowger) could be that a server is connected to two switches, one called "database-internal" and another called "sc1-pod1", which would then tell us that this server should be a database server and it's located in Pod1 in our Santa Clara DC1.

### So what is this Razor MicroKernel extension made up of?

Essentially just a few basic things:

 - A directory with "bin", "lib" and "lib/ruby" folders
 - Fedora binaries for lldpad, lldptool and dcbtool from the lldpad RPM put in the "bin" folder
 - Fedora libraries from RPMs for libconfig.so.9, liblldp_clif.so.1 and libnl.so.1 put in the "lib" folder
 - A modified version of the [openlldp.rb](https://github.com/razorsedge/puppet-openlldp/blob/master/lib/facter/openlldp.rb) file from the [razorsedge/openlldp](https://forge.puppetlabs.com/razorsedge/openlldp) module that allows you to run the lldpad daemon for a set time to be able to grab the LLDP information and push it back as facts to the Razor server, put in the "lib/ruby" folder

They are all available in the zip file, which is just a compressed version of everything in the repo.

All the binaries and libraries are distributed as-is, with no guarantee or warranty. You can and should replace them with your own.


### More information

Can be found at http://purevirtual.eu/2014/09/12/server-locality-using-razor-and-lldp/
