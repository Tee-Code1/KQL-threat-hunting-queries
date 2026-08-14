# Contributing

Queries live under one of three top-level folders, matching where they run:

- `Sentinel-KQL/` — queries against Microsoft Sentinel tables (`SigninLogs`, `SecurityEvent`, `AzureActivity`, etc.)
- `Defender-KQL/` — queries against Microsoft Defender XDR advanced hunting tables (`DeviceProcessEvents`, `DeviceNetworkEvents`, `EmailEvents`, etc.)
- `AI-KQL/` — queries detecting abuse of AI services specifically (Copilot audit logs, Azure OpenAI diagnostic logs, Defender for Cloud Apps shadow-AI signals). Use this folder even when the underlying table also appears elsewhere (e.g. `AzureActivity`, `AzureDiagnostics`) if the query's purpose is AI-service abuse detection rather than general infra hunting.

If a query works in both Sentinel and Defender (Defender tables are queryable from Sentinel via the unified XDR connector), place it in `Defender-KQL/` and note the dual compatibility in the header.

For AI-specific techniques, prefer citing **MITRE ATLAS** alongside or instead of ATT&CK in the header where a technique is genuinely AI-specific (e.g. prompt injection, cost/resource harvesting against a deployed model) - ATLAS is the AI-adapted counterpart to ATT&CK and is more precise for that threat class.

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
