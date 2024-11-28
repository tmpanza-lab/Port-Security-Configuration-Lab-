# Port Security Configuration – Lab 

## Objective

The objective of this lab exercise is to understand and implement Port Security on a campus network, a crucial step in securing access to the network. This involves configuring and managing port security settings on network switches to restrict unauthorized devices from connecting to the network. 

### Skills Learned

- Learning the Fundamentals of Port Security.
- Configuring Port Security on Switch Interface.
- Exploring Port Security Modes (Protect, Restrict, Shutdown).
- Specifying Allowed MAC Addresses.
- Testing and Verifying Port Security.
- Responding to Security Violations.


### Tools Used

- Cisco IOS Vendor-specific CLI.
- Layer 2 or Layer 3 Switches (Physical or Virtual).
- Routers (Physical or Virtual).
- GNS3: For simulating network devices and configurations.
- Cisco Packet Tracer: Simplified tool for learning and configuring VLANs.
- PuTTY (Terminal Emulator Software).


## Steps

# Topology
![image](https://github.com/user-attachments/assets/99bc06cd-999c-4fbf-93c4-8168e59bfae3)
 

# Disable Unused Ports

1) Disable all unused ports on SW1. This prevents unauthorised hosts
plugging in to them to gain access to the network.

‘show ip interface brief’ shows ports FastEthernet 0/1 – 24 and GigabitEthernet 0/1 – 2. Interfaces FastEthernet 0/1 and 0/2 are in use.
 ![image](https://github.com/user-attachments/assets/efbd75eb-a4ba-4f57-a309-24f2084d6db5)

Interfaces FastEthernet 0/1 and 0/2 are in use. Shutdown all other interfaces:
![image](https://github.com/user-attachments/assets/1b558964-b243-4296-bc37-102858a2e279)
 

# Port Security Configuration

2) Configure Port Security on interface FastEthernet 0/1. Allow a maximum of two MAC addresses and manually add PC1’s MAC address to the configuration.
Important: After enabling Port Security, do not send traffic between the PCs (for example ‘ping’) until you have manually added PC1’s MAC address to the configuration. If you do, Port Security will learn PC1’s MAC address dynamically and Packet Tracer has no function to remove it.

This results in the error “Found duplicate mac-address”. In this case you have to shutdown interface Fa0/1, save the configuration, reload then add
PC1’s MAC address before enabling interface Fa0/1 again.

Shutting down the interface is necessary because PC1 sends gratuitous ARPs when its interface comes up.

We need to discover PC1’s MAC address. We can get this information from the PC itself or from the switch. Use ‘ipconfig /all’ to find it on the PC.
![image](https://github.com/user-attachments/assets/2a34d64b-2d40-4caf-a761-024784ab642f)
 

Use ‘show mac address-table’ to find it on the switch. Use ping to generate some traffic from the PC if it does not show up in the MAC address table.
![image](https://github.com/user-attachments/assets/274fff83-c354-4559-88d0-f9f6b721dd31)
 

You need to make the interface an access port before the switch will accept Port Security configuration. No VLANs are configured on the switch or specified in the lab task so leave the it in the default VLAN 1.
![image](https://github.com/user-attachments/assets/72f3e45d-78b3-4597-a39a-d7d4c62c8f3a)

 
Add the Port Security configuration.
![image](https://github.com/user-attachments/assets/7a0672a5-85e9-4d6a-a226-9e0227db601c)

 

3) Enable Port Security on interface FastEthernet 0/2 with the default settings.
![image](https://github.com/user-attachments/assets/a49638d6-577f-425e-8de6-8cca0572d5be)
 

4) From PC1 or PC2, generate some traffic between the PCs.

Ping from PC2 to PC1 or vice versa:
![image](https://github.com/user-attachments/assets/20b4aafd-07e7-42f5-8af2-45213abd7802)
 

5) On SW1, use a ‘show port-security’ command to verify if the MAC address of PC2 has been learned by Port Security.
![image](https://github.com/user-attachments/assets/bd05e274-6a87-4fde-b625-f59dbc42c983)
 
PC2’s MAC address is 0000.2222.2222

6) Verify the full Port Security configuration on both interfaces. Do not use
the ‘show running-config’ command in this task.
![image](https://github.com/user-attachments/assets/71407703-63b6-4f46-bb24-1d201016eb67)

