# 🔍 Custom Port Scanner

A fast, multi-protocol Python port scanner with a clean GUI — supporting TCP, UDP, and SYN scanning across single IPs, CIDR ranges, and IP dash-ranges.

---

## ✨ Features

- **Three scan modes** — TCP connect scan, UDP scan, and raw SYN scan
- **Async TCP scanning** — concurrent scanning via `asyncio` for high throughput
- **Multi-host support** — scan a single IP, a CIDR block (`192.168.1.0/24`), or a dash range (`192.168.1.1-192.168.1.10`)
- **Banner grabbing** — pulls service banners and version info from open ports
- **Service detection** — maps port numbers to known service names
- **Tkinter GUI** — results displayed in a sortable table with host, port, service, version, and status columns
- **Distributed architecture** — parent/child node design for multi-node scanning coordination

---

## 📁 Project Structure

```
port-scanner/
├── gui_app.py        # Tkinter GUI — main entry point
├── scanner_core.py   # Core async TCP, UDP, and SYN scanning logic
├── banner_grabber.py # Connects to open ports and extracts service banners
├── service_map.py    # Maps port numbers to service names
├── parent_node.py    # Orchestrates distributed scanning across child nodes
└── child_node.py     # Worker node that receives and executes scan jobs
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- `tkinter` (usually bundled with Python; on Linux: `sudo apt install python3-tk`)
- No third-party packages required — uses only the standard library

### Installation

```bash
git clone https://github.com/rheasushanth/port-scanner.git
cd port-scanner
```

### Running the GUI

```bash
python gui_app.py
```

### Running a scan from code

```python
import asyncio
from scanner_core import scan_multiple_hosts

results = asyncio.run(
    scan_multiple_hosts("192.168.1.0/24", start_port=1, end_port=1024, scan_type="tcp")
)

for host, ports in results.items():
    print(f"{host}: {ports}")
```

---

## 🖥️ GUI Usage

1. Enter a target — single IP, CIDR range, or dash range
2. Set the start and end port numbers
3. Choose a scan type: **TCP**, **UDP**, or **SYN**
4. Hit **Start Scan**

Results appear in a table showing each open port's host, port number, detected service, version banner, and status.

> **Note:** SYN scanning requires root/sudo privileges on Linux.

---

## 🔬 Scan Types

| Type | Description | Notes |
|------|-------------|-------|
| **TCP** | Full async connect scan | Fast; works without elevated privileges |
| **UDP** | Sends a probe packet and awaits response | Slower; open/filtered ambiguity is expected |
| **SYN** | Raw socket half-open scan | Requires `sudo` / root on Linux |

---

## 🌐 IP Range Formats

| Format | Example |
|--------|---------|
| Single IP | `192.168.1.5` |
| CIDR | `192.168.1.0/24` |
| Dash range | `192.168.1.1-192.168.1.50` |

---

## ⚠️ Legal Disclaimer

This tool is intended for use on networks and systems you own or have explicit permission to test. Unauthorized port scanning may be illegal in your jurisdiction. Use responsibly.

---

## 📄 License

This project is open source. See [LICENSE](LICENSE) for details.
