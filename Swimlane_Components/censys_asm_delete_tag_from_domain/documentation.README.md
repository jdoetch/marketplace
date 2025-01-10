# Censys ASM - Delete Tag from a Domain

## Overview
The "Censys ASM - Delete Tag from a Domain" component provides a streamlined process for securely and efficiently removing tags from domains within the Censys Attack Surface Management (ASM) platform. This component is critical for maintaining the accuracy and relevance of domain tagging, ensuring that organizational records are up-to-date and reflect current domain categorizations.

## Summary of the Component
This component operates within the automation ecosystem to facilitate the deletion of tags from domains. It integrates seamlessly with Censys ASM, leveraging its APIs to perform tag deletions. This action is vital in scenarios where tags no longer apply to a domain due to changes in domain purpose, ownership, or security posture.

## Actions
### Action: Delete Tag
- **Type:** API Call
- **Purpose:** Removes a specified tag from a domain in Censys ASM.
- **On-Success:**
  - Logs the successful deletion.
  - Optionally triggers a notification or further actions based on configuration.
- **On-Failure:**
  - Attempts to retry the deletion.
  - Logs the failure and escalates the issue according to predefined procedures.

## Process Flow Summary
The component initiates by identifying the domain and tag combination specified by the user or another system. Once identified, it sends a request to the Censys ASM API to delete the tag. Upon successful deletion, the action logs success and, if configured, executes subsequent actions. If the deletion fails, the system logs the failure, retries the operation according to the set policy, and escalates if necessary.

Efficiency, security, and compliance are at the forefront of this process, ensuring that the tag management within Censys ASM enhances the organization's ability to accurately manage their digital assets.

