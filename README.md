# Active Directory Domain Controller

Windows Server 2022 promoted to a Domain Controller 
with DNS, RDS Web Access portal, and LDAP integration. 
Part of a connected hybrid enterprise lab running on 
bare metal Rocky Linux.

## Network Topology

![Topology](screenshots/project2-active-directory-topology.png)

## Status: In Progress

Full README with build steps, real issues, and lessons 
learned coming when the project is complete.

Ubuntu gateway now has a dedicated server subnet with 
inter-subnet routing configured. Windows Server 2022 
is deployed at 10.0.3.10 and promoted to Domain 
Controller. Domain lab.local is live with DNS running 
on DC01 and an OU structure in place with a dedicated 
admin account.

Four real issues hit along the way:

1. The VM kept booting back into the installer. It 
turns out the ISO was still mounted in VirtualBox 
so I ejected it and the issue was fixed.

2. Inter-subnet routing broke after restoring the 
Ubuntu gateway from a snapshot which reset IP 
forwarding to 0 at runtime. I ran sysctl -p to 
reload the settings and routing came back instantly.

3. Cloud-init was silently overriding sysctl.conf 
on every reboot so I created a persistent override 
in /etc/sysctl.d/ to fix it permanently.

4. The first ICMP DROP rule was blocking reply 
packets too so I added --state NEW to only block 
outbound connections originating from the DC.

## Lab Series

- [Project 1 — Linux Enterprise Gateway](https://github.com/mansour-wade/Linux-Enterprise-Gateway) — Complete
- Project 2 — Active Directory DC — In Progress
