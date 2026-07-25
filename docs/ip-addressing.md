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

**Problem 1 — How many usable hosts in a /27?**

A `/27` has 32 total addresses (2^(32-27) = 2^5 = 32). Subtracting the
network address and broadcast address leaves **30 usable hosts**.
Example: `192.168.10.0/27` → network `192.168.10.0`, usable range
`192.168.10.1 – 192.168.10.30`, broadcast `192.168.10.31`.

**Problem 2 — Splitting 10.0.0.0/24 into two /25 subnets**

A `/25` splits a /24 exactly in half (128 addresses each, 126 usable):

| Subnet    | Network address | Usable range              | Broadcast     |
|-----------|------------------|----------------------------|----------------|
| Subnet 1  | 10.0.0.0/25      | 10.0.0.1 – 10.0.0.126       | 10.0.0.127     |
| Subnet 2  | 10.0.0.128/25    | 10.0.0.129 – 10.0.0.254     | 10.0.0.255     |

**Problem 3 — What subnet is 172.16.5.200 on, given a /26 mask?**

A `/26` block size is 64. Dividing 200 by 64 gives 3 with a remainder,
so 200 falls in the 4th block (192–255):
- Network address: `172.16.5.192`
- Usable range: `172.16.5.193 – 172.16.5.254`
- Broadcast: `172.16.5.255`
- So `172.16.5.200` belongs to the `172.16.5.192/26` subnet.