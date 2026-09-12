🛰️ Network Setup & Troubleshooting (VirtualBox + Ubuntu Server)
- VirtualBox networking is a core part of this cybersecurity lab. To ensure both internet access and controlled isolation, I configured and tested multiple network modes, validated DHCP behavior, and confirmed proper routing from the guest VM.

This section documents the exact steps, configuration files, and reasoning behind the setup.

🔧 Network Modes Used in This Lab
- VirtualBox NAT — Provides internet access by routing traffic through the host
- Host‑Only Adapter — Creates an isolated network for cybersecurity testing
- DHCP — Automatically assigns IP addresses to the VM
- Netplan — Ubuntu’s YAML‑based network configuration system
- These modes allow me to switch between connected and isolated environments depending on the task.

🧩 Problem Encountered
- When first booting the Ubuntu Server VM, the system had no internet connectivity:
- ping google.com failed
- apt update could not reach repositories
- ip a showed no valid IP address
- VirtualBox was set to Host‑Only, which intentionally provides no internet
- To install tools and update packages, I needed temporary internet access.

🛠️ Solution: Enable DHCP + Switch to NAT
- I edited the Netplan configuration file to enable DHCP on the primary interface (enp0s3):
- yaml

- network:
  - version: 2
  - renderer: networkd
  - ethernets:
    - enp0s3:
      - dhcp4: true
<img width="627" height="202" alt="image" src="https://github.com/user-attachments/assets/a1eec136-7021-4f2f-af87-763f35b4108c" />
      
- Then I applied the configuration:
- bash
- sudo netplan apply
<img width="377" height="102" alt="image" src="https://github.com/user-attachments/assets/ba2c85a0-5a85-44b6-b673-4a79db15700c" />


- After switching VirtualBox to NAT, the VM successfully obtained an IP address:
- Code
- 10.0.2.15/24
- This confirmed:
- DHCP was working
- NAT was routing traffic correctly
- The VM had full internet access
<img width="324" height="100" alt="image" src="https://github.com/user-attachments/assets/eb18a91b-f274-4513-a2ce-08f9eb0a8dbb" />


🌐 Verification Steps
- To ensure the network was fully functional, I validated:
- IP assignment using ip a
- DNS resolution using ping google.com
- Package repository access using apt update
- Routing table using ip r
- All tests passed, confirming successful connectivity.

🔒 Switching Back to Host‑Only (Cybersecurity Isolation)
- Once updates and tools were installed, I switched the VM back to Host‑Only Adapter.
- This isolates the VM from the internet, which is ideal for:
- Malware analysis
- Offensive security practice
- Network attack simulations
- Avoiding accidental outbound traffic
- Host‑Only keeps the lab safe, controlled, and self‑contained.

