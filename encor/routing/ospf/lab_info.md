# Multi-Area OSPF

## General Description

- Four OSPF areas, including the backbone.
  - ASBR at the head of the network, redistributing static address.
- Two ABRs branching from the backbone:
  - ABR1 links to Area 10 and Area 20
  - ABR2 links to Area 30
- Combination of transit and stub areas:
  - Areas 20 and 30 are Transit
    - Area 20:
      - R2
      - R3
    - Area 30:
      - R4
      - R5
  - Area 10 is a stub
    - R1
- ASBR1 will redistribute a default route to Null0 just to have something there

## IP Addressing

### Loopback Addresses

| Router | Loopback Address |
| ------ | ---------------- |
| ASBR1  | 192.168.1.1/32   |
| BB1    | 192.168.1.2/32   |
| BB2    | 192.168.1.3/32   |
| ABR1   | 192.168.1.4/32   |
| ABR2   | 192.168.1.5/32   |
| R1     | 192.168.1.6/32   |
| R2     | 192.168.1.7/32   |
| R3     | 192.168.1.8/32   |
| R4     | 192.168.1.9/32   |
| R5     | 192.168.1.10/32  |

### Area 0

| Area 0        | IP Range     |
| ------------- | ------------ |
| ASBR1 <-> BB1 | 10.0.0.0/30  |
| ASBR1 <-> BB2 | 10.0.0.4/30  |
| BB1 <-> BB2   | 10.0.0.8/30  |
| BB1 <-> ABR1  | 10.0.0.12/30 |
| BB2 <-> ABR2  | 10.0.0.16/30 |

### Area 10

| Area 10     | IP Range     |
| ----------- | ------------ |
| ABR1 <-> R1 | 10.10.0.0/30 |

### Area 20

| Area 20     | IP Range     |
| ----------- | ------------ |
| ABR1 <-> R2 | 10.20.0.0/30 |
| R2 <-> R3   | 10.20.0.4/30 |

### Area 30

| Area 30     | IP Range     |
| ----------- | ------------ |
| ABR2 <-> R4 | 10.30.0.0/30 |
| R4 <-> R5   | 10.30.0.4/30 |
