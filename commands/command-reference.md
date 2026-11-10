# Command Reference

Run each command only in the VM/terminal indicated by the workflow.

| Command | Where to run it | Purpose |
|---|---|---|
| `sudo ./lab.support.files/scripts/configure_as_dhcp.sh` | CyberOps Workstation shell | Configure DHCP |
| `ifconfig` | CyberOps Workstation shell | Verify interface/IP configuration |
| `ping www.cisco.com` | CyberOps Workstation shell | Test connectivity |
| `sudo ./lab.support.files/scripts/cyberops_extended_topo_no_fw.py` | CyberOps Workstation shell | Start Mininet topology |
| `xterm R1` | `mininet>` prompt | Open an R1 terminal |
| `xterm H5` | `mininet>` prompt | Open an H5 terminal |
| `xterm H10` | `mininet>` prompt | Open an H10 terminal |
| `./lab.support.files/scripts/start_snort.sh` | R1 terminal | Start Snort IDS |
| `./lab.support.files/scripts/mal_server_start.sh` | H10 terminal | Start lab test server |
| `netstat -tunpa` | H10 terminal | Check listening services |
| `tail -f /var/log/snort/alert` | Second R1 terminal | Monitor IDS alerts |
| `wget 209.165.202.133:6666/W32.Nimda.Amm.exe` | H5 terminal | Request the lab test file |
| `tcpdump -i H5-eth0 -w nimda.download.pcap &` | H5 terminal | Capture traffic to a PCAP |
| `fg` then `Ctrl+C` | H5 terminal | Stop background tcpdump |
| `ls -l nimda.download.pcap` | H5 terminal | Verify PCAP file |
| `iptables -L -v` | R1 terminal | List firewall chains/rules |
| `iptables -I FORWARD -p tcp -d 209.165.202.133 --dport 6666 -j DROP` | R1 terminal | Insert example DROP rule |
| `quit` | `mininet>` prompt | Exit Mininet |
| `sudo mn -c` | CyberOps Workstation shell | Clean up Mininet |

## Terminal identification
- `mininet>` means commands are being entered at the Mininet CLI.
- `[analyst@secOps ~]$` is an example CyberOps Workstation user shell.
- `[root@secOps ...]#` is an example root shell inside a Mininet host/router terminal.

Prompt formats can vary. Check which window is active before running a command.
