# Contributing

Queries live under one of two top-level folders, matching where they run:

- `Sentinel-KQL/` — queries against Microsoft Sentinel tables (`SigninLogs`, `SecurityEvent`, `AzureActivity`, etc.)
- `Defender-KQL/` — queries against Microsoft Defender XDR advanced hunting tables (`DeviceProcessEvents`, `DeviceNetworkEvents`, `EmailEvents`, etc.)

If a query works in both (Defender tables are queryable from Sentinel via the unified XDR connector), place it in `Defender-KQL/` and note the dual compatibility in the header.

## File naming

`Title-Case-With-Hyphens.kql`, named after the behavior detected (e.g. `LOLBins-Making-Outbound-Network-Connections.kql`), not the underlying table.

## Header template

Every `.kql` file starts with a comment block:

```
// Title: <short, descriptive>
// Description: <what it detects and why it matters, 2-4 lines>
// MITRE ATT&CK: <Txxxx (Technique Name), ...>
// Data source: <tables/connectors required>
// False positives: <known noisy conditions or legitimate activity that trips this>
```

Then the query itself, with inline `//` comments on any non-obvious filtering logic or thresholds.
