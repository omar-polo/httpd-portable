# OpenBSD httpd, portable version

**this is an unofficial port of OpenBSD httpd!**

## Building

httpd depends on:

 - yacc/bison
 - libtls (either from LibreSSL or libretls)
 - libevent

The compilation is the usual:

	./configure
	make
	make install

httpd needs the user `_httpd` to be present on the system.  At the
moment, there's no way to change the expected username other than
modify the sources.


## Per-OS notes:

 - freebsd: the IPV6_MINHOPCOUNT setsockopt option is absent, so the
   `tcp` option `ip minttl` is ignored for IPv6 sockets.  Likewise,
   the `tcp [no] sack` option is also ignored (regardless of the IP
   version.)
