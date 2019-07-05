# What is Split-Horizon DNS?

In [computer networking](https://en.wikipedia.org/wiki/Computer_networking),
**split-horizon DNS**, **split-view DNS**, **split-brain DNS**, or
**split DNS** is the facility of a [Domain Name
System](https://en.wikipedia.org/wiki/Domain_Name_System) (DNS) implementation to provide
different sets of DNS information, usually selected by the source
address of the DNS request.

This facility can provide a mechanism for security and privacy
management by logical or physical separation of DNS information for
network-internal access (within an [administrative
domain](https://en.wikipedia.org/wiki/Administrative_domain), e.g., company) and access
from an unsecure, public network (e.g. the
[Internet](https://en.wikipedia.org/wiki/Internet)).

Implementation of split-horizon DNS can be accomplished with
hardware-based separation or by software solutions. Hardware-based
implementations run distinct DNS server devices for the desired access
granularity within the networks involved. Software solutions use either
multiple DNS server processes on the same hardware or special server
software with the built-in capability of discriminating access to [DNS
zone](https://en.wikipedia.org/wiki/DNS_zone) records. The latter is a common feature of
many server software implementations of the DNS protocol (cf.
[Comparison of DNS server
software](https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software)) and is
sometimes the implied meaning of the term *split-horizon DNS*, since all
other forms of implementation can be achieved with any DNS server
software.

## Split-Horizon DNS and DNSSEC

Split-horizon DNS is designed to provide different authoritative answers
to an identical query and [DNSSEC](https://en.wikipedia.org/wiki/DNSSEC) is used to ensure
veracity of data returned by the Domain Name System. These apparently
conflicting goals create the potential for confusion or false security
alerts in poorly constructed networks. Research has produced
recommendations to properly combine these two DNS features. [\[1\]](#cite-note-1)

## Use Case

One common use case for split-horizon DNS is when a server, *host1* in
the example below, has both a private IP address on a local area network
(not reachable from most of the Internet) and a public address, i.e. an
address reachable across the Internet in general. By using split-horizon
DNS the same name can lead to either the private IP address or the
public one, depending on which client sends the query. This allows for
critical local client machines to access a server directly through the
local network, without the need to pass through a router. Passing
through fewer network devices improves the network latency.

Internal DNS view, the server is named host1.example.net:
```
@       IN SOA  ns.example.net admin.example.net. (
                                2010010101      ; serial
                                        1D      ; refresh 
                                        1H      ; retry
                                        1W      ; expire
                                        3H )    ; minimum
@       IN      NS              ns
ns      IN      A               203.0.113.2
host1   IN      A               10.0.0.10
```
External view:
```
@       IN SOA  ns.example.net admin.example.net. ( 
                                2010010101      ; serial 
                                        1D      ; refresh 
                                        1H      ; retry
                                        1W      ; expire
                                        3H )    ; minimum 
@       IN      NS              ns
ns      IN      A               203.0.113.2
host1   IN      A               203.0.113.10
```
## See also

- [Comparison of DNS server
software](https://en.wikipedia.org/wiki/Comparison_of_DNS_server_software)
- [Split horizon route
advertisement](https://en.wikipedia.org/wiki/Split_horizon_route_advertisement)

## References
<span id="cite-note-1"></span>
[1]  [Split-View DNSSEC Operational
Practices](http://tools.ietf.org/html/draft-krishnaswamy-dnsop-dnssec-split-view)

## External links

- [Providing "split horizon" DNS
service](https://web.archive.org/web/20160528185434/http://homepage.ntlworld.com./jonathan.deboynepollard/FGA/dns-split-horizon.html).
- [BIND 9 Configure Views To Partition External and Internal DNS
Information](http://www.cyberciti.biz/faq/linux-unix-bind9-named-configure-views/).
- [Providing "split horizon" DNS service on OS X Server
systems](https://jonbrown.org/blog/10-6-2-split-horizon-dns/) (as of
OS X Server version 10.6.2).
- [Detailed How-to on DNS Views on
Bind 9](http://www.howtoforge.com/two_in_one_dns_bind9_views).

[Category:Domain name system](https://en.wikipedia.org/wiki/Category:Domain_name_system)
    
_This page uses material from the Wikipedia article <a href="https://en.wikipedia.org/wiki/Split-horizon_DNS">"Split-horizon DNS"</a>, which is released under the <a href="https://creativecommons.org/licenses/by-sa/3.0/">Creative Commons Attribution-Share-Alike License 3.0</a>._
