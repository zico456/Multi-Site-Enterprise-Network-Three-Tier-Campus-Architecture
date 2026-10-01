<h> Multi-Site-Enterprise-Network-Three-Tier-Campus-Architecture </h>

# Multi-Site-Enterprise-Network-Three-Tier-Campus-Architecture

The project models a small enterprise with a resilient HQ campus, two router-on-a-stick branches, centralized infrastructure services, dynamic routing, and controlled public access. HQ-R1 is intentionally a collapsed core/edge device because the requested design has one core/edge router; HQ-DSW1/2 perform campus Layer-3 distribution and redundant first-hop gateway service. The design is educational rather than fully production-high-availability: dual distribution switches, dual-homed access switches,HSRP, Rapid PVST+, and LACP protect campus paths, but HQ-R1, each branch router, and ISP-R1 remain explicit single points of failure.


<h>COMMON IOS BASELINE</h>
Apply this baseline to every router and switch, changing only the hostname. Generate RSA keys only after the hostname and domain name are set.
enable
configure terminal
hostname<device name>
no ip domain-lookup
enable secret zicoccna@
service password-encryption
service timestamps log datetime msec
banner motd # WARNING: Authorized administrators only. #
username zico privilege 15 secret tombilly
ip domain-name itnlab.com
crypto key generate rsa modulus 2048
ip ssh version 2
line console 0
login local
logging synchronous
exec-timeout 10 0
line vty 0 15
login local
transport input ssh
exec-timeout 10 0

<h>Enterprise-device management ACL</h>

On HQ-R1, both distribution switches, both HQ access switches, both branch routers, and both branch access switches, create
the ACL below and apply it to the VTY lines. This allows SSH only from HQ management VLAN 99. 

ip access-list standard SSH-MGMT
permit 10.10.99.0 0.0.0.255
deny any 
line vty 0 15
access-class SSH-MGMT in

<h>ISP management ACL</h>

ISP-R1 is outside NAT. Permit only the translated HQ-R1 address instead of VLAN 99 directly.
ip access-list standard SSH-MGMT
permit 198.51.100.1
deny any 
line vty 0 15
access-class SSH-MGMT in

<h>Logging on enterprise IOS devices</h>
logging host 10.10.30.10
logging trap debugging

<h>Close each IOS configuration</h>

end

copy running-config startup-config





