# Suricata Lab Notes

## Environment

- Operating system: Parrot OS
- Suricata version: 7.0.10
- Monitoring interface: `wlo1`
- Configuration file: `/etc/suricata/suricata.yaml`
- Custom rule file: `/etc/suricata/local.rules`

## Work Completed

1. Identified the active network interface.
2. Configured `HOME_NET` for the local lab network.
3. Configured Suricata's packet capture interface.
4. Validated the configuration using Suricata test mode.
5. Updated the Emerging Threats Open ruleset.
6. Checked service status and Suricata logs.
7. Verified packet capture and decoder counters.
8. Created a custom ICMP detection rule.
9. Added the custom rule file to the configuration.
10. Restarted Suricata.
11. Generated four ICMP Echo Requests in a controlled test.
12. Confirmed four matching alerts in `fast.log`.

## Log Files

- `fast.log`: human-readable detection alerts.
- `eve.json`: structured event data, including supported protocol events and alerts.
- `stats.log`: Suricata performance and processing statistics.
- `suricata.log`: Suricata operational messages and errors.

## Key Learning

Packet capture, event logging, and alert generation are different functions.

Suricata can capture and decode traffic without generating an alert. An alert is produced when traffic matches an enabled detection rule and the relevant detection and output settings are working.
