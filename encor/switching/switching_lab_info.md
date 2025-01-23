# Switching

## Overview

- Multi-switch environment
- Proper implementation and management of VLANs
  - It's for a Cisco exam, so we'll use RPVST+
  - I want some industry-standard tech involved, so LACP for EtherChannel
    - For this, I want to keep things relatively simple and focus on implementation rather than design
    - Thus, our STP Root switches will have two-link bundles to a central switch, which will in turn have a two-link bundle to an uplink switch
- As mentioned above, we have plural Root switches: one acting as a primary for one cluster of VLANs, the other acting as primary for the rest
- Port Security on access links
  - Max 2
  - I wanted to hardcode the MAC address of the currently connected device, but due to the nature of CML, I decided to go with sticky addresses
  - Shutdown on violation
- PortFast and BPDUGuard on access links

## VLAN Configuration

### VLANs

| VLAN | Workgroup        |
| ---- | ---------------- |
| 10   | IT               |
| 20   | HR               |
| 30   | Sales            |
| 40   | Customer Service |
| 50   | Accounting       |
| 80   | Native           |
| 99   | Management       |
| 100  | Blackhole        |

### Spanning-Tree

- ROOT1
  - Primary for VLANs 10, 30, 50
- ROOT2
  - Primary for VLANs 20, 40, 80, 99
- Secondaries are vice versa

### Notes

- I wanted to simulate something with actual purpose, so each VLAN is assigned to a fictional department within an organization
- While I doubt it's often used in a contemporary production network, I decided to implement a Blackhole VLAN to hold all of my unused interfaces instead of just assigning them to other VLANs and pretending they were in use, or leaving them untouched in VLAN 1.

## Addressing

### Inter-VLAN Routing Subinterfaces

| VLAN | IPv4 Address |
| ---- | ------------ |
| 10   | 10.0.10.1    |
| 20   | 10.0.20.1    |
| 30   | 10.0.30.1    |
| 40   | 10.0.40.1    |
| 50   | 10.0.50.1    |
| 80   | 10.0.80.1    |
| 99   | 10.0.99.1    |

### Management SVIs

| Switch | Address     |
| ------ | ----------- |
| ROOT1  | 10.0.99.10  |
| ROOT2  | 10.0.99.20  |
| SW1    | 10.0.99.111 |
| SW2    | 10.0.99.112 |
| SW3    | 10.0.99.113 |
| SW4    | 10.0.99.114 |
| SW5    | 10.0.99.115 |
| SW6    | 10.0.99.116 |
