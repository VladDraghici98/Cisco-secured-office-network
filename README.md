# Cisco-secured-office-network
Cisco Packet Tracer lab demonstrating network segmentation and security hardening
Segmented and Secured Office Network | Cisco Packet Tracer

Network segmentation: Segmented a two-switch office LAN into Sales, IT and Management VLANs by creating the VLANs and assigning access ports with switchport access vlan, so each department got its own broadcast domain and subnet (192.168.10.0, 192.168.20.0, 192.168.99.0 /24).
Trunking: Connected the switches and router with 802.1Q trunks, restricting allowed VLANs to 10, 20 and 99 and moving the native VLAN to an unused VLAN 999, which carried all VLAN traffic over single links and reduced VLAN-hopping risk.
Inter-VLAN routing: Configured router-on-a-stick with dot1Q subinterfaces on R1, one per VLAN, so hosts in different VLANs communicated through the router (verified with successful pings PC1→PC3 and PC2→PC4).
DHCP: Set up a DHCP server on R1 with separate pools for Sales and IT and excluded ranges for static addresses, so client PCs received addresses automatically (verified with show ip dhcp binding).
Port security: Enabled port security with sticky MAC learning, a maximum of 2 addresses and restrict violation mode on access ports, so only learned devices could use each port (verified with show port-security).
Hardening: Shut down unused ports and placed them in the unused VLAN 999, reducing the attack surface (verified with show interfaces status).
Secure remote access: Replaced Telnet with SSH v2 (local users, RSA 2048-bit keys) and restricted the VTY lines to the Management VLAN with an ACL, so only Admin-PC could manage R1, SW1 and SW2; a test from a Sales PC was rejected.
Troubleshooting: Diagnosed and fixed four faults with show commands and static-IP isolation tests: port security rejected on dynamic ports, VLANs not applied on one switch, a typo in the DHCP excluded-address range that exhausted both pools, and missing SSH credentials. Result: all hosts received DHCP leases and full connectivity was restored.
