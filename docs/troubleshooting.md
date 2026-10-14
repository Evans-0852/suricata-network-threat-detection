# Troubleshooting Notes

## 1. Incorrect Network Interface

**Problem:** Suricata initially reported that `eth0` could not be found.

**Cause:** The configured interface name did not exist on the system.

**Resolution:** Identified the active interface using:

```bash
ip addr
```

Then configured Suricata to monitor `wlo1`.

## 2. Custom Rule File Not Found

**Problem:** Suricata warned that it could not find `local.rules` under `/var/lib/suricata/rules/`.

**Cause:** The file had been created under `/etc/suricata/`, while Suricata was resolving the relative rule path under a different directory.

**Resolution:** Updated the `rule-files` section to reference the absolute path:

```yaml
rule-files:
  - suricata.rules
  - /etc/suricata/local.rules
```

Then validated the configuration again.

## 3. Empty Alert Log

**Problem:** The `fast.log` file initially contained no alert entries.

**Explanation:** Capturing packets does not automatically generate alerts. An enabled detection rule must match traffic that Suricata can inspect.

**Resolution:** Created a custom ICMP rule and generated controlled ping traffic to verify alert generation.

## 4. Ping to the Local Machine Did Not Trigger the Rule

**Problem:** Pinging the machine's own IP did not produce the expected alert.

**Explanation:** Traffic destined for the local machine may not traverse the physical interface being monitored.

**Resolution:** Tested traffic directed toward another host on the authorized local network.

## Useful Commands

Validate configuration:

```bash
sudo suricata -T -c /etc/suricata/suricata.yaml
```

Check service status:

```bash
sudo systemctl status suricata --no-pager
```

Inspect operational logs:

```bash
sudo tail -n 40 /var/log/suricata/suricata.log
```

Inspect alerts:

```bash
sudo tail -n 10 /var/log/suricata/fast.log
```

Filter for the custom rule:

```bash
sudo grep 'LAB ICMP traffic detected' /var/log/suricata/fast.log
```

Always consider timestamps when reading logs because older entries may belong to a previous service run.
