# Minimal IPTABLES firewall

## Client configuration

The file `iptables.up.client.rules` contains a minimal configuration for client configuration:

_this configuration does not limit to a specific network interface_

### ACCEPTs

- INPUT
  - all on `lo` loopback interface
  - Allow already established tcp & udp connections
  - icmp (ping) requests and replies

- FORWARD
  -nothing (default DROP)

- OUTPUT
  -all (trust internal users)

### DROPs

It obviously drops all the rest.

## Server configuration

The file `iptables.up.server.rules` contains a minimal configuration for basic server configuration:

_this configuration limits rules to a specific network interface `eth0`_

### ACCEPTs

- INPUT
  - all on `lo` loopback interface
  - Allow new tcp connection on ports 80/443 (http/https web server) and 22 (ssh server) on `eth0` interface
  - Allow already established tcp & udp connections
  - Allow new udp connection on port 53 (dns server) on `eth0` interface
  - icmp (ping) requests and replies

- FORWARD
  -nothing (default DROP)

- OUTPUT
  -all (trust internal users)

### DROPs

It obviously drops all the rest.

### Extra

### Prevent DoS Attack

Limits a maximum of 50 connection per minute after a total of 100 connection reached. 

### Logs dropped packets

Dropped packets are logged in a limit of 2 per minute with a log-level of 7

## Installation

- Copy the `iptables.up.client.rules` or `iptables.up.server.rules` file in your `/etc` directory

```
$ (sudo) cp iptables.up.client.rules /etc/iptables.up.rules
```

- Copy the startup script `iptables.startup` in the `/etc/network/if-pre-up.d/` directory

```
$ (sudo) cp iptables.startup /etc/network/if-pre-up.d/iptables
$ (sudo) chmod +x /etc/network/if-pre-up.d/iptables
```


## References

- http://crm.vpscheap.net/knowledgebase.php?action=displayarticle&id=29
- https://wiki.debian.org/iptables

