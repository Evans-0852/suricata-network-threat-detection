# Suricata Test Results

## Test: Custom ICMP Detection Rule

**Objective:** Verify that Suricata detects ICMP Echo Requests directed toward the configured home network.

**Rule SID:** `1000001`

**Alert message:** `LAB ICMP traffic detected`

**Test method:** Generated four ICMP Echo Requests using `ping -c 4` against another host on the authorized local lab network.

**Expected result:** Suricata should generate an alert for each matching Echo Request that it captures.

**Observed result:** Four matching alert lines appeared in `fast.log`.

## Conclusion

The test confirmed that the custom ICMP rule loaded and generated alerts for the test traffic observed by Suricata.

The result validates this specific rule and test scenario. It does not guarantee that all network traffic is visible or that all threats will be detected.

## Additional Observations

- Packet capture and decoder counters increased during network activity.
- DNS query and response events were recorded.
- TLS metadata was recorded for an observed connection.
- The inspected statistics snapshot showed zero kernel capture drops at that time.

## Evidence

Redacted screenshots of the configuration validation, service status, custom rule, and matching alerts can be added to the `screenshots/` directory.
