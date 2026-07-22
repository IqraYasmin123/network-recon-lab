# IP Addressing Practice

## Public vs Private IP

**Private ranges (RFC 1918)** — not routable on the public internet, used
behind NAT:

| Range                       | CIDR         | Usable hosts |
|------------------------------|--------------|--------------|
| 10.0.0.0 – 10.255.255.255     | 10.0.0.0/8   | ~16.7M       |
| 172.16.0.0 – 172.31.255.255   | 172.16.0.0/12| ~1M          |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16| ~65k        |

**Public IPs** — globally unique, routable, assigned by an ISP/RIR.

## Subnetting Basics

- A **/24** network (e.g., `192.168.1.0/24`) = 256 total addresses,
  254 usable host addresses (1 network address + 1 broadcast reserved).
- Subnet mask `255.255.255.0` = /24.
- CIDR notation `/n` = number of bits used for the network portion.

### Practice: splitting a /24 into four /26s

`192.168.1.0/24` → four subnets of `/26` (64 addresses each, 62 usable):

| Subnet             | Network address  | Usable range                  | Broadcast        |
|---------------------|------------------|--------------------------------|-------------------|
| Subnet 1            | 192.168.1.0/26   | 192.168.1.1 – 192.168.1.62     | 192.168.1.63      |
| Subnet 2            | 192.168.1.64/26  | 192.168.1.65 – 192.168.1.126   | 192.168.1.127     |
| Subnet 3            | 192.168.1.128/26 | 192.168.1.129 – 192.168.1.190  | 192.168.1.191     |
| Subnet 4            | 192.168.1.192/26 | 192.168.1.193 – 192.168.1.254  | 192.168.1.255     |

### My own practice problems

_(Add 2–3 subnetting problems you worked through by hand here, with your
answers — good evidence of practice for the submission.)_
