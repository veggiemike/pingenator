Pingenator - a super ping tool to get you places
================================================

Copyright 2021-2022 Michael D Labriola <veggiemike@sourceruckus.org>

Licensed under the GPLv3. See the file COPYING for details. 

Pingenator's primary use-case is checking internet connectivity by pinging a
list of hosts.  The pinging is done in parallel, so you can ping a dozen hosts
once and have the results in 1 second instead of 12.

Get the latest and greatest from https://github.com/sourceruckus/pingenator.

<pre>
usage: pingenator [-h] [-V] [-v] [-q] [-d] [-e IP] [-c N] [-s PERCENT] [-g IP]
                  [IPADDR [IPADDR ...]]

positional arguments:
  IPADDR                IP address to ping.

optional arguments:
  -h, --help            show this help message and exit
  -V, --version         show program's version number and exit
  -v, --verbose         Be verbose. Can be supplied multiple times for
                        increased levels of verbosity.
  -q, --quiet           Be quiet. Only output is "N of N reached".
  -d, --dns             Additionally use built-in IPs of Public DNS servers
                        provided by Google, Cloudflare, Quad9, OpenDNS, and
                        Comodo Secure DNS.
  -e IP, --exclude IP   Do not ping specified IP, even if it's been specified.
                        This can be used to exclude IPs added via the --dns
                        flag. Can be specified multiple times.
  -c N, --count N       Send N ping packets. Default is 1. Specifying 0 will
                        cause each ping subprocess to ping continiously.
  -s PERCENT, --success PERCENT
                        Return successfully if percentange reached is at least
                        PERCENT. Special case 0 means success if any responses
                        are received. Default is 0.
  -g IP, --gateway IP   Use the specified gateway IP for outgoing pings. This
                        causes a static route to be added to the system for
                        each IP to be pinged, so admin privileges are
                        required. Routes are removed at the end, so there
                        shouldn't be any lasting effect, but care should be
                        taken that you don't accidentally make an important
                        host unreachable while testing (i.e., don't use a
                        gateway to test an alternate WAN interface pinging the
                        DNS server your system is currently using).

For example, to send 4 pings in parallel to each public DNS server
provided by Google, Cloudflare, Quad9, OpenDNS, and Comodo Secure DNS,
exluding 8.8.8.8, using 10.1.99.1 as an alterate gateway, treating a
reply-rate of 90% as success, and get the results all whithin about 1
second:

  pingenator --dns --exclude 8.8.8.8 --count 4 --success 90 --gateway 10.1.99.1

Or, to ping a couple hosts continuously using an alterate gateway:

  pingenator -g 192.168.5.1 -c0 8.8.4.4 1.1.1.1
</pre>
