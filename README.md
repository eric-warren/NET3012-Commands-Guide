# NET3012-Commands-Guide
## Configuration
### Card/MDA:

show card

show mda

configure card 1 card-type iom3-xp

configure card 1 mda 1 mda-type m10-1gb-xp-sfp

configure card 1 mda 1 no shutdown

### Port:

configure port 1/1/X no shutdown

### Interface

configure router interface {name} address {address}

configure router interface {name} loopback

configure router interface {name} port {port}

configure router interface {name} loopback

### Static Routes:

configure router static-route {remote network /mask} next-hop {next-hop-address}

### OSPF:

configure router router-id <32-bit-ID>

configure router ospf area <area #> interface <interface name> interface-type <point-to-point>

configure router ospf area 0 nssa

configure router ospf area 0 stub

configure router ospf area 2 stub no summaries (totally stubby area)

configure router ospf export {Policy Name}

configure router ospf traffic-engineering

configure router ospf rsvp-shortcut

###### 


-over-RSVP

configure router ospf ldp-over-rsvp

configure router ospf asbr

### LDP:

configure router ldp no shutdown

configure router ldp interface-parameters interface <interface-name>

configure router ldp-shortcut

configure router ldp shortcut-local-ttl-propagate (turns on uniform mode for local traffic)

configure router ldp no shortcut-local-ttl-propagate (turns on pipe mode for local traffic)

configure router ldp shortcut-transit-ttl-propagate (turns on uniform mode for transit traffic)

configure router ldp no shortcut-transit-ttl-propagate (turns on pipe mode for transit traffic)

###### T-LDP

configure router ldp targeted-session peer 10.10.10.9 {tunneling}

### ECMP:

configure router ecmp {max-ecmp-routes}

### BGP:

configure router autonomous-system {AS Number}

configure router bgp group <group-id> neighbor {IP-address} peer-as {AS-#}

configure router bgp group <group-id> next-hop-self

configure router bgp export <policy-stmt>

###### BGP Next-hop resolution with tunnels

configure router bgp next-hop-resolution shortcut-tunnel family ipv4 resolution any

### Policy Statement:

configure router policy-options begin

configure router policy-options policy-statement <policy name> entry <number> from protocol {direct | ospf | bgp | isis | rip}

configure router policy-options policy-statement <policy name> entry <number> to protocol {direct | ospf | bgp | isis | rip}

configure router policy-options policy-statement <policy name> entry <number> action {accept | next-entry | next-policy | reject}

exit

configure router policy-options commit

### RSVP:

configure router mpls no shutdown

configure router rsvp no shutdown

configure router mpls interface {interface name} no shutdown

###### Path Creation

configure router mpls path pathToRx shutdown

configure router mpls path pathToRx hop 10 10.10.10.6 {strict | loose}

configure router mpls path pathToRx no shutdown

###### Creation of LSP

configure router mpls lsp lspToRx shut

configure router mpls lsp lspToRx to 10.10.10.x

configure router mpls lsp lspToRx cspf

configure router mpls lsp lspToRx primary <Path Name> [include green] no shutdown

configure router mpls lsp lspToRx secondary <Path Name> [exclude red] no shutdown

configure router mpls lsp lspToRx secondary <Path Name> [standby] no shutdown

configure router mpls lsp lspToRx no shutdown

###### PIPE mode vs Uniform mode

configure router rsvp shortcut-local-ttl-propagate (turns on uniform mode for local traffic)

configure router rsvp no shortcut-local-ttl-propagate (turns on pipe mode for local traffic)

configure router rsvp shortcut-transit-ttl-propagate (turns on uniform mode for transit traffic)

configure router rsvp no shortcut-transit-ttl-propagate (turns on pipe mode for transit traffic)

### Link Coloring:

configure router if-attribute admin-group green value 1

configure router mpls interface toR3 admin-group red

### IPv6 (6pe):

configure router interface "ToR9" ipv6 (link local)

configure router interface "system" ipv6 address fd00:7:7::5/128

###### OSPFv3 config

configure router ospf3 area 0 interface "system" interface-type point-to-point

configure router ospf3 area 0 interface "system" no shutdown

configure router ospf3 asbr

configure router ospf3 no shutdown

###### LDP IPv6

configure router ldp interface-parameters interface "toR4" dual-stack ipv4 no shutdown

###### MP-BGP config

configure router autonomous-system {AS Number}

configure router bgp group "R5ToR7" family ipv6

configure router bgp group "R5ToR7" peer-as 65507

configure router bgp group "R5ToR7" neighbor 10.10.10.7 advertise-label ipv6

configure router bgp no shutdown

### Epipe

#### CE:

configure port 1/1/2 shut

configure port 1/1/2 ethernet encap-type dot1q

configure port 1/1/2 no shut

configure router interface toR5_10 address 192.168.10.9/24

configure router interface toR5_10 port 1/1/2:10

#### PE:

configure port 1/1/2 shut

configure port 1/1/2 ethernet mode access

configure port 1/1/2 ethernet encap-type dot1q

configure port 1/1/2 no shut

configure service sdp {sdp-id} mpls create

&nbsp;&nbsp;&nbsp; far-end 10.10.10.x

&nbsp;&nbsp;&nbsp; ldp

&nbsp;&nbsp;&nbsp; lsp {lsp-name}

&nbsp;&nbsp;&nbsp; no shut

&nbsp;&nbsp;&nbsp; exit

configure service customer 1 create

&nbsp;&nbsp;&nbsp; exit

configure service epipe {service-id} customer 1 create

&nbsp;&nbsp;&nbsp; sap 1/1/2:{q-tag} create

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shut

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp; spoke-sdp {sdp-id}:{vc-id} create

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shut

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp; no shut

### VPLS:

#### CE:

configure port 1/1/2 shut

configure port 1/1/2 ethernet encap-type dot1q

configure port 1/1/2 no shut

configure router interface toR5_10 address 192.168.10.9/24

configure router interface toR5_10 port 1/1/2:10

#### PE:

configure port 1/1/2 shut

configure port 1/1/2 ethernet mode access

configure port 1/1/2 ethernet encap-type dot1q

configure port 1/1/2 no shut

configure service sdp {sdp-id} mpls create

&nbsp;&nbsp;&nbsp; far-end 10.10.10.x

&nbsp;&nbsp;&nbsp; ldp

&nbsp;&nbsp;&nbsp; lsp {lsp-name}

&nbsp;&nbsp;&nbsp; no shut

&nbsp;&nbsp;&nbsp; exit

configure service customer 1 create

&nbsp;&nbsp;&nbsp; exit

configure service vpls {service-id} customer 1 create

&nbsp;&nbsp;&nbsp; sap 1/1/2:{q-tag} create

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shut

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp; mesh-sdp {sdp-id} create

&nbsp;&nbsp;&nbsp; no shut

&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp; spoke-sdp {sdp-id}:{vc-id} create

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shut

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp; no shut

&nbsp;&nbsp;&nbsp; exit

### IES

#### IES Core router

configure service ies x000 customer 1 create

&nbsp;&nbsp;&nbsp;interface toRx_ies create

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;address 172.17.X.1/24

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ip-mtu 1500

&nbsp;&nbsp;&nbsp;spoke-sdp X:x000 create

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no shut

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit

&nbsp;&nbsp;&nbsp;no shut

&nbsp;&nbsp;&nbsp;exit

#### CE

configure router ospf area 0 interface "toRX" mtu 1500

### VPRN

#### PE:

configure router autonomous-system 64496

configure router bgp

&nbsp;&nbsp;&nbsp; group MPBGP

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; family vpn-ipv4

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; neighbor 10.10.10.y peer-as 64496

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; local-address 10.10.10.x

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shutdown

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp; no shutdown


configure service customer {110/120} create

&nbsp;&nbsp;&nbsp; description {Blue/Red}

&nbsp;&nbsp;&nbsp; exit


vprn {serv#} customer {cus#} create

&nbsp;&nbsp;&nbsp; description VPRN for {Blue/Red}

&nbsp;&nbsp;&nbsp; router-id 10.10.10.x

&nbsp;&nbsp;&nbsp; auto-bind-tunnel resolution-filter ldp

&nbsp;&nbsp;&nbsp; auto-bind-tunnel resolution filter

&nbsp;&nbsp;&nbsp; auto-bind-tunnel any

&nbsp;&nbsp;&nbsp; route-distinguisher 64496:{110/120}

&nbsp;&nbsp;&nbsp; vrf-target target:64496:{110/120}

&nbsp;&nbsp;&nbsp; interface toRX_VPRN create

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; address 10.x.x.x/24

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; sap 1/1/2:{110/120} create

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shutdown

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shutdown

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp exit

&nbsp;&nbsp;&nbsp; no shutdown


configure router policy-options

&nbsp;&nbsp;&nbsp; begin

&nbsp;&nbsp;&nbsp; policy-statement mpbpg-bgp

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entry 10

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; from protocol bgp-vpn

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; action accept

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp;exit

&nbsp;&nbsp;&nbsp;commit


configure service vprn {serv#}

&nbsp;&nbsp;&nbsp; shutdown

&nbsp;&nbsp;&nbsp; autonomous-system 64496

&nbsp;&nbsp;&nbsp; bgp

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; group toRX_CE_BGP

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; neighbor 10.x.x.x peer-as XXXXX

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; export mpbpg-bgp

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shutdown

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shutdown

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp; no shutdown


#### CE:

configure router interface to_Rx-{110/120}

&nbsp;&nbsp;&nbsp; port 1/1/2:{110/120}

&nbsp;&nbsp;&nbsp; address 10.x.x.x/24

&nbsp;&nbsp;&nbsp; no shutdown

&nbsp;&nbsp;&nbsp; exit


configure router policy-options

&nbsp;&nbsp;&nbsp; begin

&nbsp;&nbsp;&nbsp; policy-statement direct-bgp

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; entry 10

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; from protocol direct

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; to protocol bgp

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; action accept

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp; exit

commit


configure router

&nbsp;&nbsp;&nbsp; autonomous-system XXXXX

&nbsp;&nbsp;&nbsp; bgp

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; group toRX_PE

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; neighbor 10.x.x.x peer-as 64496

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; export direct-bgp

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; no shutdown

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; exit

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no shutdown

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;exit

&nbsp;&nbsp;&nbsp; no shutdown

### Resilience

configure router mpls lsp <lsp-name> secondary <path-name>  # Def'n of secondary
  
configure router mpls lsp <lsp-name> secondary <path-name> standby  # (hot) standby
  
configure router mpls lsp <lsp-name> fast-reroute facility   # Bypass tunnel
  
### SRLG

configure router if-attribute srlg-group <name> value {number} # Definition of the group
  
configure router mpls interface <name> srlg-group <name> # Define link membership
  
configure router mpls lsp <name> cspf # Enable CSPF; NEEDED!
  
configure router mpls lsp <name> secondary <path> srlg # Enable use of SRLG


## Troubleshooting

### Search for a Command

tree flat | match "keyword"

### General Commands

show router status

show router route-table

show router tunnel-table

telnet <management ip address>
  
ping <ip-address>
  
traceroute <ip-route>
  
oam lsp-ping prefix <ip-address>
  
oam lsp-trace prefix <ip-address>
  
oam ldp-treetrace prefix <ip-address>
  
show router ecmp

### Port Commands

show port

show port 1/1/x [detail]

### Interface Commands

show router interface

show router interface "int-name" detail

show router interface summary

### OSPF Commands

show router ospf status

show router ospf routes

show router ospf opaque-database

show router ospf neighbor

show router ospf interface

show router ospf database

show router ospf area {area-num} [detail]

### LDP Commands

show router ldp status

show router ldp bindings [active]

show router ldp parameters

show router ldp discovery [detail] 

show router ldp interface

show router ldp session

clear router ldp session <neighbor-ip-address>

### MPLS/RSVP Commands

tools perform router mpls resignal lsp <lsp-name> path <path-name>

show router mpls status

show router mpls path

show router mpls lsp [detail]

show router mpls lsp <lsp-name> path detail
  
show router mpls interface

show router rsvp status

show router rsvp session

show router rsvp interface [detail]

show router rsvp neighbor

## Config Checklist

### General

- Configure and no shut ports
- Ensure interfaces have right ips and ports
- Configure a router ID

### RSVP
- ensure IGP is working
- OSPF Traffic engineering

### BGP
- Ensure a autonomous system is configured

### LDP over RSVP
- T-ldp from abr to abr 
- LSP from abr to abr 
- enable ldp over rsvp

### 6PE
- Configure ospv3
- Ensure to put in asbr command
- COnfigure epxort policies in both directions

### EPIPE
- Configure CE with dot1q and no shut
- On ce configure interface with 1/1/1:XXX
- On PE configure ethernet mode access and dot1q
- Configure Customer
- Configure sdp and enabled ldp in sdp if using ldp
- Configure sap and spoke-sdp

### VPLS
- Configure CE with dot1q and no shut
- On ce configure interface with 1/1/1:XXX
- On PE configure ethernet mode access and dot1q
- Configure Customer
- Configure sdp and enabled ldp in sdp if using ldp
- Configure sap and spoke/mesh sdp

### IES
- Change MTU in IES
- CHnage ospf MTU

### VPRN
- Use family vpn-ipv4 MPBGP
- configure router-id in service
- Set RD and RT
