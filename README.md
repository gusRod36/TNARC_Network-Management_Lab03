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

## Key decisions

## Verification

## Challenges and fixes

## Limitations

## What I'd do next

