# Campus–Edge Home Lab

**Stack:** Cisco 2800/2960G/2950/3750 • HSRP • eBGP • ZBF • CoPP • DHCP/NAT • SNMPv3/Syslog/NTP • NetFlow • DHCP Snooping/DAI/IPSG • Port-security

![Topology](diagrams/topology.png)

## IP Plan
See [ip-plan/vlans-and-subnets.md](ip-plan/vlans-and-subnets.md)

## What this shows
- Redundancy: HSRP (+ IP SLA)
- Routing: eBGP (R1↔R2, R1↔R3) with optional MD5
- Security: ZBF (stateful), CoPP (control-plane), AAA local, SNMPv3 only
- Services: DHCP/NAT on R1, Syslog/NTP, NetFlow v9
- L2 guardrails: DHCP Snooping, DAI/IP Source Guard, Port-security
- Core L2: LACP etherchannel SW3↔SW4, trunking 10/20/30/99/200

## Proof (validations)
See [validations/](validations/) for show outputs:
- show standby brief, show ip bgp summary
- show policy-map control-plane, show policy-map type inspect zone-pair
- show ip dhcp snooping, show interfaces trunk
- show ip nat statistics, show ip cache flow

## Reuse
1) Apply configs in configs/ to matching gear
2) Ensure trunks carry **10,20,30,99,200**; SW3↔SW4 Port-Channel up
3) Manage from VLAN10 (older IOS may need legacy SSH cipher flags)
