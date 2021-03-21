# NET3012-Commands-Guide
## Card/MDA:

show card

show mda

configure card 1 card-type iom3-xp

configure card 1 mda 1 mda-type m10-1gb-xp-sfp

configure card 1 mda 1 no shutdown

## Port:

configure port 1/1/X no shutdown

## Interface

configure router interface {name} address {address}

configure router interface {name} loopback

configure router interface {name} port {port}

configure router interface {name} loopback

## Static Routes:

configure router static-route {remote network /mask} next-hop {next-hop-address}

## OSPF:

configure router router-id <32-bit-ID>

configure router ospf area <area #> interface <interface name> interface-type <point-to-point>

configure router ospf asbr

configure router ospf traffic-engineering

configure router ospf area 0 nssa

configure router ospf area 0 stub

configure router ospf area 2 stub no summaries (totally stubby area)

configure router ospf export {Policy Name}

configure router ospf rsvp-shortcut

configure router ospf ldp-over-rsvp

## LDP:

configure router ldp no shutdown

configure router ldp interface-parameters interface <interface-name>

configure router ldp-shortcut

configure router ldp [no] shortcut-local-ttl-propagate

configure router ldp [no] shortcut-transit-ttl-propagate

configure router ldp shortcut-local-ttl-propagate (turns on uniform mode for local traffic)

configure router ldp no shortcut-local-ttl-propagate (turns on pipe mode for local traffic)

configure router ldp shortcut-transit-ttl-propagate (turns on uniform mode for transit traffic)

configure router ldp no shortcut-transit-ttl-propagate (turns on pipe mode for transit traffic)

configure router ldp targeted-session peer 10.10.10.9 {tunneling}

## ECMP:

configure router ecmp {max-ecmp-routes}

## BGP:

configure router autonomous-system {AS Number}

configure router bgp group <group-id> neighbor {IP-address} peer-as {AS-#}

configure router bgp group <group-id> next-hop-self

configure router bgp export <policy-stmt>

configure router bgp next-hop-resolution shortcut-tunnel family ipv4 resolution any

## Policy Statement:

configure router policy-options begin

configure router policy-options policy-statement <policy name> entry <number> entry 10 from protocol {direct | ospf | bgp | isis | rip}

configure router policy-options policy-statement <policy name> entry <number> entry 10 action {accept | next-entry | next-policy | reject}

## RSVP:

configure router mpls no shutdown

configure router rsvp no shutdown

configure router mpls interface {interface name} no shutdown

configure router mpls path pathToRx

hop 10 10.10.10.6 {strict | loose}

no shutdown

exit

configure router mpls lsp lspToRx

to 10.10.10.x

cspf

no shutdown

primary <Path Name> include green

secondary <Path Name> exclude red

exit

configure router rsvp shortcut-local-ttl-propagate (turns on uniform mode for local traffic)

configure router rsvp no shortcut-local-ttl-propagate (turns on pipe mode for local traffic)

configure router rsvp shortcut-transit-ttl-propagate (turns on uniform mode for transit traffic)

configure router rsvp no shortcut-transit-ttl-propagate (turns on pipe mode for transit traffic)

## Link Coloring:

configure router if-attribute admin-group green value 1

configure router mpls interface toR3 admin-group red

## IPv6:

configure router interface "ToR9" ipv6 (link local)

configure router interface "system" ipv6 address fd00:7:7::5/128

configure router ospf3 area 0 interface "system" interface-type point-to-point

configure router ospf3 area 0 interface "system" no shutdown

configure router ospf3 asbr

configure router ospf3 no shutdown

configure router ldp interface-parameters interface "toR4" dual-stack ipv4 no shutdown

configure router bgp group "R5ToR7" family ipv6

configure router bgp group "R5ToR7" peer-as 65507

configure router bgp group "R5ToR7" neighbor 10.10.10.7 advertise-label ipv6

configure router bgp no shutdown

## Epipe

### CE:

configure port 1/1/2 shut

configure port 1/1/2 ethernet encap-type dot1q

configure port 1/1/2 no shut

configure router interface toR5_10 address 192.168.10.9/24

configure router interface toR5_10 port 1/1/2:10

### PE:

configure port 1/1/2 shut

configure port 1/1/2 ethernet mode access

configure port 1/1/2 ethernet encap-type dot1q

configure port 1/1/2 no shut

configure service sdp {sdp-id} mpls create

far-end 10.10.10.x

ldp

lsp {lsp-name}

no shut

exit

configure service customer 1 create

exit

configure service epipe {service-id} customer 1 create

sap 1/1/2:{q-tag} create

no shut

exit

spoke-sdp {sdp-id}:{vc-id} create

no shut

exit

no shut

## VPLS:

### CE:

configure port 1/1/2 shut

configure port 1/1/2 ethernet encap-type dot1q

configure port 1/1/2 no shut

configure router interface toR5_10 address 192.168.10.9/24

configure router interface toR5_10 port 1/1/2:10

### PE:

configure port 1/1/2 shut

configure port 1/1/2 ethernet mode access

configure port 1/1/2 ethernet encap-type dot1q

configure port 1/1/2 no shut

configure service sdp {sdp-id} mpls create

far-end 10.10.10.x

ldp

lsp {lsp-name}

no shut

exit

configure service customer 1 create

exit

configure service vpls {service-id} customer 1 create

sap 1/1/2:{q-tag} create

no shut

exit

mesh-sdp {sdp-id} create

no shut

exit

spoke-sdp {sdp-id}:{vc-id} create

no shut

exit

no shut

exit
