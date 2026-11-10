# Step-by-Step Workflow

Follow the Cisco handout in order. This file is a working checklist, not a replacement for the instructor's lab document.

## Part 1 — Prepare the virtual environment

### 1. Configure VirtualBox
- [ ] Open VirtualBox and select **CyberOps Workstation**.
- [ ] Open **Machine → Settings → Network**.
- [ ] Configure Adapter 1 as **Bridged Adapter**, if necessary.
- [ ] If using Wi-Fi with a proxy, the handout says NAT may be needed instead.
- [ ] Ensure the network adapter is enabled and the virtual cable is connected.
- [ ] If a memory error occurs, increase VM memory; the handout suggests trying 2 GB when the default 1 GB is insufficient.

### 2. Boot and configure DHCP
- [ ] Start CyberOps Workstation and log in using the credentials supplied with your course image.
- [ ] Open a terminal.
- [ ] From the directory containing `lab.support.files`, run:

```bash
sudo ./lab.support.files/scripts/configure_as_dhcp.sh
```

- [ ] Enter the `analyst` account password when prompted.
- [ ] Verify the interface has a local-network IP address using:

```bash
ifconfig
```

- [ ] Test internet connectivity:

```bash
ping www.cisco.com
```

- [ ] Stop ping with `Ctrl+C`.
- [ ] Record the interface/IP and ping result in your notes.

## Part 2 — Firewall and IDS logs

### Step 1 — Real-time IDS log monitoring

#### 1. Start Mininet
From the CyberOps Workstation terminal, run:

```bash
sudo ./lab.support.files/scripts/cyberops_extended_topo_no_fw.py
```

Wait for the `mininet>` prompt.

#### 2. Open R1 and start Snort
At the `mininet>` prompt:

```text
xterm R1
```

In the R1 terminal, run:

```bash
./lab.support.files/scripts/start_snort.sh
```

Snort remains in the foreground. Leave this terminal running.

#### 3. Open H5 and H10
Return to the Mininet prompt and run each command:

```text
xterm H5
xterm H10
```

#### 4. Start the test server on H10
In the H10 terminal:

```bash
./lab.support.files/scripts/mal_server_start.sh
```

Verify the listening service:

```bash
netstat -tunpa
```

The Cisco example shows nginx listening on TCP port `6666`. Record your actual output.

#### 5. Monitor Snort alerts
Open another R1 terminal from the Mininet prompt:

```text
xterm R1
```

In this second R1 terminal:

```bash
tail -f /var/log/snort/alert
```

Leave the alert monitor running.

#### 6. Request the test file from H5
In H5, use the lab-provided server address and filename as shown in the Cisco handout:

```bash
wget 209.165.202.133:6666/W32.Nimda.Amm.exe
```

Record:
- Destination port used.
- Whether the file downloaded completely.
- Whether Snort generated an alert.
- Alert source and destination IP addresses.
- Alert source and destination ports.
- Alert timestamp.
- IDS signature message.

The address and filename above are the values printed in the handout. If your instructor's environment supplies different values, use the values assigned to your lab.

#### 7. Capture the transfer with tcpdump
On H5, start the capture in the background:

```bash
tcpdump -i H5-eth0 -w nimda.download.pcap &
```

Press Enter if needed, then repeat the `wget` request from H5.

Bring tcpdump to the foreground and stop it:

```bash
fg
```

Press `Ctrl+C`.

Verify the capture file exists and has a non-zero size:

```bash
ls -l nimda.download.pcap
```

Keep the PCAP inside the lab VM. The handout says analysis of this PCAP is performed in another lab.

### Step 2 — Tune firewall rules based on IDS alerts

#### 1. Open another R1 terminal
From `mininet>`:

```text
xterm R1
```

#### 2. List current firewall rules
In the new R1 terminal:

```bash
iptables -L -v
```

Record the chains shown.

#### 3. Add the blocking rule
The Cisco handout's example rule is:

```bash
iptables -I FORWARD -p tcp -d 209.165.202.133 --dport 6666 -j DROP
```

This inserts a rule in the FORWARD chain to drop TCP traffic destined for the specified server IP and destination port.

Use the server address and port that apply to your supplied lab topology. Do not apply this rule on your Windows host or an unrelated network.

#### 4. Verify the rule
Run:

```bash
iptables -L -v
```

Confirm the DROP rule appears in the FORWARD chain.

#### 5. Retry the request from H5
Run the same `wget` command again. Record whether it succeeds or times out. Stop repeated retries with `Ctrl+C` if needed.

Answer the question about a more aggressive valid blocking approach based on the lab discussion and your instructor's expectations.

## Part 3 — Terminate and clear Mininet

### 1. Quit Mininet
Return to the main CyberOps Workstation terminal showing `mininet>` and enter:

```text
quit
```

### 2. Clean up Mininet
From the CyberOps Workstation shell, run:

```bash
sudo mn -c
```

Enter the requested password when prompted.

### 3. Final checks
- [ ] Mininet has exited.
- [ ] Mininet cleanup command completed.
- [ ] Screenshots and notes are saved.
- [ ] Lab answers are completed from actual observations.
