# Censys ASM - Delete Tag from a SubDomain

## Overview
The Censys ASM - Delete Tag from a SubDomain component is an essential tool designed to manage and streamline the process of removing specific tags from subdomains within the Censys ASM environment. This component is particularly useful for maintaining clean and accurate data, and for the automation of security and data management processes.

## Component Summary
The main functionality of this component revolves around the targeted deletion of tags from subdomains, enabling users to efficiently manage their domain tagging system. The process flow ensures that tags are safely and accurately removed without impacting other associated data.

### Actions
- **Delete Tag**: The core action within this component handles the identification and removal of a specified tag from a subdomain.
  - **Type**: Transformation (processing and changing data).
  - **Purpose**: To ensure that the subdomain's metadata is updated to reflect the changes without the specified tag.
  - **On-Success**: Confirmation that the tag has been deleted.
  - **On-Failure**: Error handling and logging the failure to delete the tag.
  - **Subsequent Steps**: Update audit logs to record the deletion action.

### Process Flow Summary
1. **Initialization**: The component begins by confirming user permissions and ensuring that the subdomain exists within the system.
2. **Tag Identification**: The component identifies the tag that needs to be removed from the specified subdomain.
3. **Tag Deletion**: Executes the process to delete the tag, ensuring that no other data is affected.
4. **Verification & Logging**: Post-deletion, the component verifies that the tag has been successfully removed and updates the system logs with this action.
5. **Completion**: Successfully ends the process if the tag is deleted, or moves to error handling if the process fails.

Through this succinct yet potent workflow, the Censys ASM - Delete Tag from a SubDomain component ensures effective management and organization within the Censys ASM platform.

