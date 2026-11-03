# MotorPH Network Design (Cisco Packet Tracer)

Enterprise network for **MotorPH, a fictional company**, built as a group academic project at Mapúa Malayan Digital College (BS Information Technology, Term 1 2025-2026). Team of 3.

![MotorPH network topology](images/topology.png)

## Overview
A network for a new headquarters with 5 departments (Sales and Collection, HR, Marketing, Accounting, IT) and a guest Wi-Fi network. It connects 27 PCs, 2 laptops, 4 printers, and 5 access points.

## My role
- Built the network for 5 departments and a guest network in a team of 3: 6 VLANs, VLSM addressing from one /24, and inter-VLAN routing on a Layer 3 core switch.
- Placed an ASA firewall with NAT between the router and core, and set up dual-ISP failover with a floating static route.
- Found overlapping subnets and routing gaps during testing and fixed them using ping and show-command checks.

## Design
| Area | Details |
|---|---|
| Topology | Star: router → ASA firewall → core switch → 5 access switches |
| Segmentation | 6 VLANs, VLSM addressing from 192.168.20.0/24 |
| Routing | Inter-VLAN routing with SVIs on the Layer 3 core switch; static routes |
| Security | ASA 5505 with NAT, VLAN isolation per department |
| Redundancy | Dual ISP with floating static route; standby core switch |
| Devices | 2911 router, ASA 5505, 3650 core, 3560 standby, 2960 access switches |

## Addressing
| Department | VLAN | Subnet | Gateway |
|---|---|---|---|
| Sales and Collection | 10 | 192.168.20.0/27 | 192.168.20.1 |
| HR | 20 | 192.168.20.32/28 | 192.168.20.33 |
| Marketing | 30 | 192.168.20.48/28 | 192.168.20.49 |
| Accounting | 40 | 192.168.20.64/28 | 192.168.20.65 |
| IT | 50 | 192.168.20.80/29 | 192.168.20.81 |
| Guest Wi-Fi | 60 | 192.168.20.128/26 | 192.168.20.129 |

Transit links: Router–ASA 192.168.10.0/30, ASA–Core 192.168.10.4/30.

## Testing
- Checked VLAN port assignments with `show vlan brief`.
- Confirmed PC addressing with `ipconfig` (correct IP, mask, and gateway).
- Pinged the department gateway and another VLAN's gateway through the core switch.

## Challenges and fixes
- **Overlapping VLSM subnets** broke addressing and routing, so the plan was recalculated into non-overlapping ranges.
- **Routing gaps** between the router, ASA, and core were found with ping and show commands, then fixed with the missing static routes.

## Files
- `MotorPH.pkt`: Packet Tracer file (open with Cisco Packet Tracer)
- `docs/`: milestone documents (PDF)
- `configs/`: device configurations (passwords removed)
- `images/`: topology screenshot

## Tools
Cisco Packet Tracer
