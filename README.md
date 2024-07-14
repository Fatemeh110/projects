# Traceroute Project
The Internet is a large and complex aggregation of network hardware, connected together by gateways. Tracking the route one's packets follow (or finding the miscreant gateway that's discarding your packets) can be difficult. traceroute utilizes the IP protocol time to live field and attempts to elicit an ICMP TIME_EXCEEDED response from each gateway along the path to some host.
Traceroute is a popular debugging tool that was first developed early in the history of the Internet. It allows users to get a general sense of the path packets take through the network en route to a destination. To understand how traceroute works, first consider the Time to Live (TTL) field defined in the IP Header. The IP TTL ensures that packets do not loop indefinitely through misconfigured Internet topologies by setting an upper bound on the number of hops an IP packet can traverse. Its implementation is simple: The originator of an IP packet sets an initial TTL value to something generally above 30. Each router that receives the packet checks if TTL=1. If it is, the router generates an ICMP Time Exceeded message (see RFC 792) and sends it back to the source of the packet. Otherwise, the TTL is decremented, and the packet is forwarded to the next router.

Traceroute exploits the behavior of the IP TTL header to determine the path packets take en route to a particular destination. It does this by sending a series of probes (usually UDP packets) with incrementing TTLs. Traceroute sets the TTL of the first probe to 1. The first router in the path that receives the probe will drop it and send an ICMP Time Exceeded message back to traceroute. This Time Exceeded message has the router's IP as its source, thus revealing the router's IP to traceroute. Traceroute repeats this process, incrementing the TTL of its probes by one each time until it reveals all routers in the path.
