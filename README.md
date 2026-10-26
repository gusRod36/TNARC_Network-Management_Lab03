## TNARC HQ: Network Managment, Monitoring and DNS


## The problem
Stage 2 hardening added AAA logins and security controls, but every event stays on the device that logged it. No one sees a rogue DHCP block or a failed login unless they're on that switch. Events on different devices can't be lined up. Additionally there are no configuration backup, a failed switch would mean rebuilding from memory. Users and admins reach everything by IP address, with no internal name resolution. Leadership wants these shared services in place before any new site is connected.

## Requirements
1. Every device's clock is synchronized from one trusted source.
2. Logs from every device reach a central server, with timestamps lined up.
3. Device statistics can be read remotely (read only), and only from approved hosts.
4. Every configuration is backed up centrally, and a restore has been tested.
5. Internal DNS resolves server and network devices by name, DHCP clients get DNS server automatically.
6. Security events (port security, BPDU Guard, AAA failures) appear in central logs.

## Topology changes
| Device | Port | | Device | Port | Subnet | Change | 
|--------|------|-|--------|------|--------|--------|
| Management-Server | fa0 | -> | Server-SW1 | g1/0/5 | 10.0.200.32/28 | Added |
| AAA-Server | fa0 | -> | Server-SW1 | g1/0/4 | 10.0.200.16/28 | Subnet from 10.0.201.0/24 to 10.0.200.16/28 |
| DHCP-Server | fa0 | -> | Server-SW1 | g1/0/3 | 10.0.200.0/28 | Subnet from /24 to /28 |

## Key decisions
1. Decided to reduce the AAA server subnet to a /28 and combine it with the DHCP network. This is to waste less host addresses within the network and to help keep a clean direction for the server addresses.

2. NTP service was configured on the Management-Server using 10.0.200.35 as the IP address and CST timezone.

3. Syslog configured on the Management-Server on IP address: 10.0.200.35, it was configured to debugging trap level, timestamps enabled and all switches are synched with NTP.

## Verification

## Challenges and fixes
1. I realized it was a mistake to make the DHCP server into the 10.0.200.0/24 subnet so I switched it to 10.0.200.0/28, this allowed me to change the AAA-Server from 10.0.201.0/24 to 10.0.200.16/28. The mistake was a short sight and should have been avoided from the beginning, however it is best to fix it now.

2. Cisco Packet Tracer lacks clock commands support so I had rely definitively on the Server NTP service and network synching together. This at the very least gave me equal timing across the network.

## Limitations

## What I'd do next
