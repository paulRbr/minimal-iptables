# Minimal IPTABLES firewall

The file `iptables.up.rules` contains a minimal configuration that exhaustively does:

## ACCEPTs

- INPUT
  - all on `lo` loopback interface
  - tcp ports 443 (https) and 22 (ssh) from everywhere on `eth0` interface
  - icmp (ping) requests and replies
  - udp port 53 (dns) outbound from `eth0` interface

- FROWARD
  -nothing (default DROP)

- OUTPUT
  -all (trust internal users)

## DROPs

It obviously drops all the rest.

## Extra

### Prevent DoS Attack

Limits a maximum of 50 connection per minute after a total of 100 connection reached. 

### Logs dropped packets

Dropped packets are logged in a limit of 2 per minute with a log-level of 7


# Installation

- Copy the `iptables.up.rules` file in your `/etc` directory

    $ (sudo) cp iptables.up.rules /etc/

- Copy the startup script `iptables.startup` in the `/etc/network/if-pre-up.d/` directory

    $ (sudo) cp iptables.startup /etc/network/if-pre-up.d/iptables
    $ (sudo) chmod +x /etc/network/if-pre-up.d/iptables



# Sources

- http://crm.vpscheap.net/knowledgebase.php?action=displayarticle&id=29
- https://wiki.debian.org/iptables

