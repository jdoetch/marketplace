# Symantec DLP - Get Policy Matches

## Overview

This document provides detailed technical documentation for the Symantec DLP - Get Policy Matches component. Designed to add an asset and pass in an incident ID to retrieve the Symantec incident policy matches, this component serves a critical function in ensuring compliance and monitoring data leakage within an organization.

## Component Description

The "Symantec DLP - Get Policy Matches" component is designed to interact with Symantec's Data Loss Prevention software. It retrieves specific policy matches related to incidents, which are crucial for compliance audits and preventive measures against data loss.

### Actions

#### Get Policy Matches
- **Type:** Connector
- **Description:** Adds an asset and passes in an incident ID to retrieve policy matches.
- **Inputs:**
  - **path_parameters:**
    - **id:** Incident ID
  - **verify_ssl:** A boolean that checks the SSL certificate.
- **Process Flow:**
  - **On-Success:** Proceeds to the next steps if available.
  - **On-Failure:** Handles errors or failures in the process.
  - **On-Complete:** Executes any completion routines.

#### Component Result
- **Type:** Transformation
- **Description:** Manages the transformation of the data retrieved from the Get Policy Matches action.
- **Process Flow:**
  - **On-Success:** N/A
  - **On-Failure:** N/A
  - **On-Complete:** N/A

### Overall Process Flow Summary

1. **Initialization:** An incident ID is specified.
2. **Action Execution:** The component executes the "Get Policy Matches" action using the provided incident ID.
3. **Data Transformation:** Transforms the data retrieved to be utilized in further processes or reporting.
4. **Completion:** The component completes the execution and returns the resultant data.

## Conclusion

The "Symantec DLP - Get Policy Matches" component plays a vital role in the security architecture by allowing for the detailed analysis of policy matches against incidents detected by Symantec DLP. This ensures that organizations can respond promptly and effectively to potential data breaches and maintain compliance with relevant data protection regulations.

