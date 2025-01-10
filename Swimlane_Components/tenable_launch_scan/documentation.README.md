# Tenable - Launch Scan

## Short Description

This component enables security teams to initiate vulnerability scans using Tenable.io by automating the launch of scans and monitoring their status. It streamlines the vulnerability management process by validating scan inputs, executing scan launches, and retrieving real-time scan statuses. Robust error handling ensures reliable and efficient operations, enhancing the overall security posture.

## Summary

The **Tenable - Launch Scan** component automates the process of initiating vulnerability scans within Tenable.io. The workflow begins by validating the provided scan ID to ensure it meets the necessary criteria. Upon successful validation, the component launches the specified scan using Tenable.io's API. It then monitors the scan's status, providing real-time updates on the scan's progress and completion. Comprehensive error handling mechanisms are in place to capture and record any issues that arise during the scan initiation or status retrieval processes, ensuring the reliability and integrity of vulnerability management operations.

## Actions and Their Purpose

### Tenable Launch Scan
**Type:** connector  
**Purpose:** Initiates a vulnerability scan in Tenable.io using the provided scan ID.

**On Success:** Calls Tenable_Scan_Status.

**Inputs:**
- path_parameters: 
  - scan_id: References the Scan_ID input.

**Action:** tenable_io.launch_scan

### Tenable Scan Status
**Type:** connector  
**Purpose:** Retrieves the current status of a launched vulnerability scan from Tenable.io.

**On Success:** No subsequent actions.

**Inputs:**
- path_parameters: 
  - scan_id: References the Scan_ID input.

**Action:** tenable_io.get_scan_status

### Update Result Variable
**Type:** updateVariables  
**Purpose:** Updates the result variable with the scan UUID, status, and progress obtained from the Tenable.io actions.

**Inputs:**
- scan_uuid: References the Tenable_Launch_Scan.result.json_body.scan_uuid
- status: References the Tenable_Scan_Status.result.json_body.status
- progress: References the Tenable_Scan_Status.result.json_body.progress

**On Success:** The component’s execution concludes successfully.

## Process Flow Summary

1. **Initialization:** The component begins by receiving the Scan_ID as input.
2. **Scan Launch:** It initiates a vulnerability scan in Tenable.io using the provided Scan_ID.
3. **Status Retrieval:** Upon successfully launching the scan, it retrieves the current status and progress of the scan.
4. **Result Compilation:** The component compiles the scan UUID, status, and progress into the result variable.
5. **Finalization:** Updates the result variable, concluding the component successfully.
6. **Error Handling:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final scan details stored in the result variable.
Component: component_aDYkPJCVZxVy8zcPS_playbook

Summary
This component facilitates the process of launching a scan on Tenable.io and monitoring its status. It first triggers the launch of a scan using the provided Scan_ID, then checks the status of the launched scan to track its progress and final state. The component outputs the scan's UUID, status, and progress, allowing users to monitor the scan lifecycle.

Actions
Tenable_Launch_Scan
Type: Connector

Purpose: This action is responsible for initiating a scan on Tenable.io using the provided Scan_ID.

Subsequent Steps: 

On Success: Triggers the Tenable_Scan_Status action to retrieve the status of the launched scan.

On Failure: No defined subsequent steps.

On Complete: No defined subsequent steps.

Inputs:

Scan_ID: A unique identifier for the scan to be launched. This ID is passed as part of the path parameters.

Pool: Default pool ($default)

Asset: Tenable_io

Action: tenable_io.launch_scan

Tenable_Scan_Status
Type: Connector

Purpose: This action retrieves the status of a scan that was launched using the Tenable_Launch_Scan action. It checks the current progress and final status of the scan.

Subsequent Steps: 

On Success: No defined subsequent steps.

On Failure: No defined subsequent steps.

On Complete: No defined subsequent steps.

Inputs:

Scan_ID: The unique identifier for the scan, passed as part of the path parameters.

Pool: Default pool ($default)

Asset: Tenable_io

Action: tenable_io.get_scan_status

Process Flow Summary
Tenable_Launch_Scan is triggered with the Scan_ID as input. This action initiates a scan on Tenable.io.

Upon successful initiation of the scan, the component proceeds to the Tenable_Scan_Status action, which checks the current status of the scan.

The results of the Tenable_Scan_Status action include the scan's status and progress. These outputs are published for further use.

The component outputs the following:

scan_uuid: The unique identifier of the scan returned by the Tenable_Launch_Scan action.

status: The current status of the scan retrieved from Tenable_Scan_Status.

progress: The progress of the scan, also retrieved from Tenable_Scan_Status.

Inputs
Scan_ID: A string representing the unique identifier of the scan to be launched. This ID can be used to initiate and track the scan's progress.

Outputs
scan_uuid: The unique identifier for the scan, which is generated when the scan is launched.

status: The current status of the scan, as retrieved from Tenable.io.

progress: The current progress of the scan, expressed as a percentage.

Entry Points
The entry point for this component is the Tenable_Launch_Scan action. It begins the process of launching the scan and tracking its status.

Additional Information
Timeout: No timeout is specified for this component.

Publish: The component publishes the following outputs:

scan_uuid: The unique identifier of the launched scan.

status: The scan's current status.

progress: The scan's current progress.