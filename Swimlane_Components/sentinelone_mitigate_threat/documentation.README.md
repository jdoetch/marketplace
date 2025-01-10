This Swimlane component enables automated mitigation of identified threats in SentinelOne, providing a streamlined approach to threat response. After attempting the mitigation action, it generates a concise string summary, ideal for record display and operational tracking within workflows.

**Usage:**

- Configure SentinelOne asset

- Get a Threat ID from a SentinelOne

- Add the component to the workflow

- Pass in Threat ID, and the valid mitigation action

- Receive a summary back confirming it was completed

- Can store the summary in a record for later reference

**Valid Mitigation Actions:**

- network-quarantine

- un-quarantine

- remediation

- kill

- quarantine

- rollback-remediations