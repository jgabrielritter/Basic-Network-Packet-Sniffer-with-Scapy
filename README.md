# Network Packet Sniffer

A Python-based network packet analysis tool with both command-line and graphical interfaces.

![Network Packet Sniffer](https://github.com/yourusername/network-packet-sniffer/raw/main/screenshots/gui_preview.png)

## Overview

This Network Packet Sniffer allows you to capture and analyze network traffic in real-time. It provides detailed information about packets at various network layers (Link, Network, Transport) and identifies common protocols and services.

## Features

- Real-time packet capture and analysis
- Support for multiple network interfaces
- BPF (Berkeley Packet Filter) syntax for targeted capture
- Protocol identification (ARP, IP, TCP, UDP, ICMP)
- Service detection (HTTP, HTTPS, DNS, SSH, FTP, DHCP)
- Packet statistics and information
- Save captured packets to PCAP files for further analysis
- Available as both command-line tool and GUI application

## Requirements

- Python 3.6+
- Scapy
- Tkinter (for GUI version)
- Root/Administrator privileges (for capturing on most interfaces)

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/network-packet-sniffer.git
   cd network-packet-sniffer
   ```

2. Install dependencies:
   ```
   pip install scapy
   ```

## Usage

### Command-Line Interface

```
python3 packet_sniffer.py [-h] [-i INTERFACE] [-c COUNT] [-f FILTER] [-o OUTPUT]
```

Arguments:
- `-i, --interface`: Network interface to use (default: system default)
- `-c, --count`: Number of packets to capture (0 for infinite, default: 0)
- `-f, --filter`: BPF filter to apply (e.g., "tcp port 80")
- `-o, --output`: Output file to save captured packets (PCAP format)

Example:
```
# Capture 10 HTTP packets on eth0
sudo python3 packet_sniffer.py -i eth0 -c 10 -f "tcp port 80"
```

### Graphical Interface

```
sudo python3 packet_sniffer_gui.py
```

1. Select a network interface from the dropdown menu
2. Optionally enter a BPF filter expression
3. Set maximum packet count (0 for unlimited)
4. Optionally specify an output file path
5. Click "Start Capture" to begin

## Understanding the Output

The tool provides detailed information about each captured packet:

- **Timestamp**: When the packet was captured
- **Link Layer (Layer 2)**: ARP information if applicable
- **Network Layer (Layer 3)**: IP addresses, TTL
- **Transport Layer (Layer 4)**: TCP/UDP ports and flags
- **Application Layer**: Identified services
- **Summary**: Brief packet description
- **Size**: Packet size in bytes

## BPF Filter Examples

- Capture only TCP traffic: `tcp`
- Capture HTTP traffic: `tcp port 80`
- Capture DNS traffic: `udp port 53`
- Capture traffic from/to a specific IP: `host 192.168.1.1`
- Capture traffic on a subnet: `net 192.168.1.0/24`
- Combine filters: `tcp port 80 or tcp port 443`

## Advanced Usage

### Saving Packets

Both the CLI and GUI versions support saving captured packets to PCAP files. These files can be opened with tools like Wireshark for more detailed analysis.

### Running with Required Privileges

Most packet capturing operations require administrative privileges:

- **Linux/macOS**: Run with `sudo`
- **Windows**: Run Command Prompt or PowerShell as Administrator

### Analyzing Specific Protocols

Use the BPF filter to target specific protocols:
```
# Capture only ICMP (ping) traffic
sudo python3 packet_sniffer.py -f "icmp"
```

## Troubleshooting

### "Permission denied" error
- Make sure you're running the tool with administrator/root privileges

### Interface not found
- Check if the interface name is correct
- Some virtual interfaces may not support packet capture

### No packets captured
- Verify your filter syntax
- Ensure there is active traffic on the selected interface
- Check firewall settings that might block packet capturing

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Disclaimer

This tool is intended for educational purposes and legitimate network analysis. Always ensure you have permission to capture and analyze network traffic on the target network.
