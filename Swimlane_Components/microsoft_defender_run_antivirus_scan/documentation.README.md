# Microsoft Defender - Run Antivirus Scan Component

## Overview
The Microsoft Defender - Run Antivirus Scan Component is designed to automate the process of initiating antivirus scans using Microsoft Defender. It is capable of handling both quick and full scans based on specified conditions. This document describes the function and flow of the component, detailing each action within the component's architecture, its purpose, the types of inputs and outputs each action expects, and how each action is linked to subsequent steps.

## Description of Actions
### Create Variables
- **Type:** Create Variables
- **Purpose:** Initializes variables to be used throughout the component flow.
- **On Success:** Proceeds to Full or Quick Scan condition check.
- **On Failure:** No subsequent action.

### Full or Quick Scan
- **Type:** Conditional
- **Purpose:** Determines whether a full or quick scan should be initiated based on input conditions.
- **On Success:** Triggers either "Run Full Antivirus Scan" or "Run Quick Antivirus Scan" based on the scan type condition.
- **On Failure:** No subsequent action.

### Run Full Antivirus Scan
- **Type:** Connector (Microsoft Defender)
- **Purpose:** Executes a full antivirus scan using Microsoft Defender.
- **On Success:** Checks the status code result and proceeds accordingly.
- **On Failure:** No subsequent action.

### Run Quick Antivirus Scan
- **Type:** Connector (Microsoft Defender)
- **Purpose:** Executes a quick antivirus scan using Microsoft Defender.
- **On Success:** Triggers condition check regarding the scan's success.
- **On Failure:** No subsequent action.

### Defender Status Code
- **Type:** Conditional
- **Purpose:** Evaluates the response of the antivirus scan.
- **On Success:** Updates variables based on the scan type that was executed (Full or Quick).
- **On Failure:** No subsequent action.

### Update Variables for Full Scan
- **Type:** Update Variables
- **Purpose:** Updates system variables based on the results from the Full Antivirus Scan.
- **On Success:** No further actions.
- **On Failure:** No further actions.

### Update Variables for Quick Scan
- **Type:** Update Variables
- **Purpose:** Updates system variables based on the results from the Quick Antivirus Scan.
- **On Success:** No further actions.
- **On Failure:** No further actions.

## Process Flow Summary
The component begins by creating necessary variables. Depending on conditions defined, it either initiates a full scan or a quick scan using Microsoft Defender. Post-scan actions evaluate the result and update the system variables accordingly. This component provides a structured way to automate routine scans and handle the results for further processing or auditing.

## Reason for Existence
The Microsoft Defender - Run Antivirus Scan Component exists to automate the process of managing antivirus scan activities with Microsoft Defender, ensuring systematic, consistent, and efficient handling of cybersecurity measures on a network or individual system basis. Automation provides timely execution and response handling, augmenting the security framework while minimizing manual oversight and potential human error.

