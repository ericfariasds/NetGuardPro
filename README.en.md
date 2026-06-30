# NetGuard Pro

[🇧🇷 Português](./README.md) | [🇪🇸 Español](./README.es.md)

Real-time network management and security monitor, protect, and optimize your infrastructure from a single dashboard.

NetGuard Pro continuously monitors your servers' performance (CPU, memory, disk, latency, packet loss), triggers automatic failover when failures occur, and protects your network with a configurable firewall and threat detection.

---

## Table of Contents

- [Getting Started](#getting-started)
- [Key Features](#key-features)
- [Use Case: Reducing Downtime with Failover](#use-case-reducing-downtime-with-failover)
- [Project Structure](#project-structure)
- [For Developers: API Integration](#for-developers-api-integration)
- [How to Contribute](#how-to-contribute)
- [Troubleshooting](#troubleshooting)
- [Support](#support)
- [License](#license)

---

## Getting Started

### Requirements

- Ubuntu Linux 20.04+ or Windows Server 2019+
- 8 GB RAM (16 GB recommended for production)
- Docker installed
- Outbound access through port 443

### Installation

```bash
git clone https://github.com/netguardpro/netguard-pro.git
cd netguard-pro
docker compose up -d
```

### First Access

1. Open `http://localhost:8080` in your browser.
2. Create your administrator account.
3. Add the first server to monitor (IP address + credentials).
4. Done! Within a few seconds, metrics will begin appearing on the dashboard.

> **Tip:** Start by monitoring only 1–2 critical servers before adding your entire infrastructure. This makes it easier to validate alerts and firewall rules without unnecessary noise.

---

## Key Features

| Feature | Description |
| --- | --- |
| **Real-time Monitoring** | Tracks CPU, memory, disk, latency, and packet loss for each server |
| **Automatic Failover** | Redirects traffic to a backup service when the primary one fails |
| **Load Balancing** | Distributes requests across servers to prevent overload |
| **Configurable Firewall** | Creates access rules based on IP, port, or service |
| **Threat Detection** | Identifies suspicious activity with prioritized alerts |
| **Custom Dashboard** | Allows each team to choose which metrics are highlighted |

---

## Use Case: Reducing Downtime with Failover

**Scenario:** An IT team runs a critical authentication service on a single server. During a traffic spike, the primary server starts failing.

**With NetGuard Pro:**

1. The system detects the performance degradation through continuous monitoring (high latency and error rate).
2. Automatic failover redirects requests to the backup server within seconds.
3. An alert is sent to the team, including the metrics history that triggered the transition.
4. The team confirms through the dashboard that the service has stabilized without manual intervention.

**Result:** Downtime is reduced from minutes to seconds, while the team gains full visibility into the root cause without manually investigating logs.

---

## Project Structure

```text
netguard-pro/
├── api/              # REST endpoints and authentication logic
├── monitor/          # Metrics collection (CPU, memory, disk, network)
├── failover/         # Detection and automatic failover logic
├── firewall/         # Rules engine and validation
├── dashboard/        # Dashboard frontend (React)
├── docs/             # Technical documentation
├── tests/            # Automated tests
└── docker-compose.yml
```

Each module has its own `README.md` with implementation details. Start with `monitor/` and `api/` if this is your first contribution—they are the best documented modules.

---

## For Developers: API Integration

The REST API allows you to retrieve metrics and manage configurations programmatically.

```bash
curl -X GET "https://api.netguardpro.com/v1/metrics?server=srv-01" \
  -H "Authorization: Bearer YOUR_TOKEN_HERE"
```

Expected response:

```json
{
  "server": "srv-01",
  "cpu_usage": 68.4,
  "latency_ms": 112.3,
  "packet_loss": 0.4
}
```

Complete endpoint, authentication, and rate limit documentation: [`docs/api.md`](docs/api.md).

---

## How to Contribute

1. **Open an issue** describing the bug or enhancement before you start coding.
2. **Create a branch** from `main`: `feature/feature-name` or `fix/bug-name`.
3. **Follow the project's coding standards:** ESLint for the frontend (`dashboard/`) and PEP 8 for Python modules (`monitor/`, `failover/`).
4. **Write tests** for every new feature or bug fix (`tests/`).
5. **Open a Pull Request** including:
   - A clear description of the changes and their purpose
   - A reference to the related issue
   - Confirmation that all tests pass (`docker compose run tests`)
6. A maintainer will review your PR within three business days.

Complete coding guidelines: [`docs/contributing.md`](docs/contributing.md).

---

## Troubleshooting

| Problem | Possible Cause | Solution |
| --- | --- | --- |
| Dashboard becomes slow under heavy load | High CPU usage during advanced analysis | Reduce the dashboard refresh frequency in `Settings > Performance` |
| Firewall configuration is confusing | Learning curve of the rule interface | Use the guided setup wizard in `Firewall > New Wizard` |
| Too many security alerts | Low-priority events are being reported | Adjust severity levels in `Alerts > Priorities` |
| Large data transfers are slow | Bandwidth congestion during traffic peaks | Enable manual prioritization in `Bandwidth > Rules` |

---

## Support

- **Full Documentation:** [`docs/`](docs/)
- **Help Center:** suporte.netguardpro.com
- **Report a Bug:** Open an issue in this repository
- **Urgent Technical Support:** suporte@netguardpro.com

---

## License

This project is distributed under the MIT License. See [`LICENSE`](LICENSE) for details.
