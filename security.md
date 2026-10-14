# Security Policy

This repository is intended for educational and defensive security purposes.

## Safe Use

- Monitor only systems and networks you own or are authorized to monitor.
- Use controlled, harmless traffic for detection testing.
- Review log files and screenshots before publishing them.
- Do not commit passwords, API tokens, private keys, or credentials.
- Avoid publishing unnecessary internal or public IP addresses, MAC addresses, or other sensitive network details.
- Do not upload raw packet captures or full logs unless they have been reviewed and sanitized.

## Scope

The included custom rule detects ICMP Echo Requests directed toward `HOME_NET`. It is a benign detection rule and does not exploit or modify target systems.

## Limitations

A successful test demonstrates the behavior of the tested rule under the tested conditions. It does not establish complete network visibility or comprehensive threat detection.
