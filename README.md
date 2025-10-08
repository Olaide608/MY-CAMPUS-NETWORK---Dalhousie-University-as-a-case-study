# MY-CAMPUS-NETWORK---Dalhousie-University-as-a-case-study
<img width="3200" height="1966" alt="MY CAMPUS NETWORK" src="https://github.com/user-attachments/assets/a3622b9d-49c2-4e11-bcee-cc1764b08d21" />

The project is evolving - I’ll keep updating as I configure more features

The objective of this project is to demonstrate several network protocols I explored during the summer, using a conceptual model of Dalhousie University’s campus LAN with a primary focus on Sexton Campus. The design incorporates both Layer 2 and Layer 3 technologies, including iBGP, OSPF, FHRP, RIP, Static Routing, DHCP, VTP, and VLAN.

At the core layer, three routers represent the Sexton, Studley, and Truro campuses, positioned as if within a central data center. Although Sexton is the main focus, Studley and Truro were introduced to provide redundancy and high availability. Both connect directly to the NAT for internet access, with dedicated DHCP interfaces for switch connectivity. Sexton connects to Studley and Truro via OSPF (Area 0 – Backbone Area), while a static route provides direct connectivity to the NAT. Studley is configured as the primary path (AD=2) and Truro as the backup (AD=10). An iBGP full-mesh was also deployed across the core routers to enable reachability between Studley and Truro, which are not physically connected.

At the distribution layer, gateway redundancy is provided via HSRP on two Layer-3 switches (LS1 and LS2), which also handle failover and aggregate access-layer traffic into the Sexton core. LS1 has a higher HSRP priority (see HSRP documentation for verification). RIP is used between the distribution switches and is redistributed into OSPF at the core to ensure consistent routing across the network. VTP is configured on both switches within the same domain, allowing access-layer switches to automatically identify the active switch if one fails. VLANs are assigned per department, with each department using two VLANs—one for wireless access points and one for wired LAN connectivity - and a WLC will later be integrated to manage APs once hardware limitations are resolved.

Additionally, SolarWinds NPM has been installed for network monitoring and discovery, but hardware limitations have delayed full configuration. The system will be updated once these issues are resolved.
