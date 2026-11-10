# Lab Overview — Snort and Firewall Rules

## Objectives
- Prepare the virtual environment.
- Examine firewall and IDS logs.
- Terminate and clear the Mininet process.

## Background
The lab introduces firewall rules and IDS signatures. Firewall rules commonly inspect packet headers, while IDS signatures may inspect packet payloads. Both use matching conditions and actions.

## Required resources
- CyberOps Workstation virtual machine
- Internet connection

## Topology and components
The supplied CyberOps Workstation hosts the Mininet environment. The lab uses:
- **R1** — router/firewall device running Snort and `iptables`.
- **H5** — host used to request the test file and capture traffic.
- **H10** — host simulating the server.
- **Mininet** — creates the lab network and host terminals.

## Main activities
1. Configure CyberOps Workstation networking using the supplied DHCP script.
2. Start the extended Mininet topology.
3. Start Snort on R1 and monitor `/var/log/snort/alert`.
4. Start the test web server on H10.
5. Request the test file from H5 and observe Snort alerts.
6. Capture the transfer to a PCAP file with `tcpdump`.
7. Inspect the existing `iptables` chains and add a rule to drop TCP traffic to the lab server on port 6666.
8. Retry the request and verify that it is blocked.
9. Quit Mininet and clean up its processes.

## Important notes
- Use the CyberOps Workstation VM named in the Cisco lab, not Kali Linux, for the prescribed Mininet and Snort steps.
- The Cisco handout allows Bridged Adapter, or NAT in the stated Wi-Fi-with-proxy situation.
- The handout notes that 2 GB RAM may be needed if the default 1 GB causes memory errors.
- The example IP addresses and outputs in the handout are expected lab examples. Record what your environment actually displays.
