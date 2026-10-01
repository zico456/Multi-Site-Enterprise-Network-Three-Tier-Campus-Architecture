<h> Multi-Site-Enterprise-Network-Three-Tier-Campus-Architecture </h>
# Multi-Site-Enterprise-Network-Three-Tier-Campus-Architecture
The project models a small enterprise with a resilient HQ campus, two router-on-a-stick branches, centralized infrastructure services, dynamic routing, and controlled public access. 
HQ-R1 is intentionally a collapsed core/edge device because the requested design has one core/edge router; HQ-DSW1/2 perform campus Layer-3 distribution and redundant first-hop gateway service. The design is educational rather than fully production-high-availability: dual distribution switches, dual-homed access switches,
HSRP, Rapid PVST+, and LACP protect campus paths, but HQ-R1, each branch router, and ISP-R1 remain explicit single points of failure.
