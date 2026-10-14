# Suricata Network Intrusion Detection Lab

A hands-on Network Intrusion Detection System (NIDS) project using **Suricata 7.0.10 on Parrot OS**. This project documents the configuration of Suricata, packet monitoring, custom detection rule creation, alert verification, and troubleshooting.

## Project Overview

The objective of this project was to configure Suricata to monitor network traffic and detect selected network activity using a custom detection rule.

I configured Suricata on my Parrot OS workstation, verified packet capture, created a custom ICMP detection rule, generated controlled test traffic, and confirmed that the rule generated alerts.

## Objectives

- Install and configure Suricata.
- Identify the correct network interface for monitoring.
- Configure the local network using `HOME_NET`.
- Validate the Suricata configuration.
- Update the Emerging Threats Open ruleset.
- Create and load a custom ICMP detection rule.
- Generate controlled test traffic and verify alerts.
- Document troubleshooting steps and findings.

## Lab Environment

| Component | Details |
|---|---|
| Operating system | Parrot OS |
| Suricata version | 7.0.10 |
| Network interface | `wlo1` |
| Main configuration | `/etc/suricata/suricata.yaml` |
| Custom rules file | `/etc/suricata/local.rules` |
| Alert log | `/var/log/suricata/fast.log` |
| Event log | `/var/log/suricata/eve.json` |

Network-specific addresses have been omitted to avoid unnecessarily exposing local network details.

## Implementation

### 1. Suricata Configuration

I configured Suricata to monitor the appropriate network interface and set `HOME_NET` to the local network used in the lab.

I validated the configuration using:

```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

The configuration loaded successfully.

### 2. Update Detection Rules

I updated the detection rules using:

```bash
sudo suricata-update
```

The Emerging Threats Open ruleset was used.

### 3. Packet Capture Verification

I examined Suricata's statistics and confirmed that packet capture and packet decoding counters increased during network activity.

I also observed DNS and TLS metadata in `eve.json`.

### 4. Custom ICMP Detection Rule

I created a custom rule to detect ICMP Echo Requests directed toward `HOME_NET`.

```suricata
alert icmp any any -> $HOME_NET any (msg:"LAB ICMP traffic detected"; itype:8; sid:1000001; rev:1;)
```

The rule was saved in `local.rules` and added to the `rule-files` section of the Suricata configuration.

### 5. Test the Detection Rule

I generated four ICMP Echo Requests using a controlled ping test against another host on the local lab network.

I then checked the alert log:

```bash
sudo grep 'LAB ICMP traffic detected' /var/log/suricata/fast.log
```

**Result:** Four matching alerts were observed, confirming that the custom rule detected the test traffic visible to Suricata.

## Results

- Suricata configuration validation succeeded.
- Packet capture and decoding activity were observed.
- DNS and TLS metadata events were recorded.
- The custom ICMP rule loaded successfully.
- Four matching ICMP detection alerts were generated.
- Initial configuration and rule-path issues were investigated and resolved.

This test validates the custom ICMP rule in the tested environment. It does not demonstrate that every type of malicious traffic will be detected.

## Troubleshooting

During the project, I investigated:

- An incorrect network interface name in the capture configuration.
- A custom rule file path that did not match the configured rules directory.
- An empty alert log before the custom detection test.
- The importance of sending test traffic through an interface monitored by Suricata.

See [`docs/troubleshooting.md`](docs/troubleshooting.md) for details.

## Repository Structure

```text
suricata-network-threat-detection/
├── README.md
├── SECURITY.md
├── .gitignore
├── rules/
│   └── local.rules
├── docs/
│   ├── lab-notes.md
│   ├── test-results.md
│   └── troubleshooting.md
└── screenshots/
    └── README.md
```

## Skills Demonstrated

- Linux command-line administration
- Network interface identification
- IDS configuration and monitoring
- Suricata rule syntax
- Network traffic analysis
- Alert verification
- Troubleshooting
- Security documentation

## Future Improvements

- Add additional custom detection rules.
- Analyze alerts in greater detail.
- Explore Suricata EVE JSON event analysis.
- Build a dashboard for visualizing security events.
- Conduct additional controlled tests in an authorized lab.

## Responsible Use

This project was conducted as a learning exercise. Network monitoring and testing should only be performed on systems and networks that you own or have explicit authorization to monitor.

Raw logs, packet captures, and configuration files containing sensitive information should not be uploaded to a public repository without appropriate review and redaction.
