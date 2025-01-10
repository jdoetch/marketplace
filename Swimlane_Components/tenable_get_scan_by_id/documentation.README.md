# Tenable.IO - Get Scan By ID

## Short Description

This component enables security teams to efficiently retrieve detailed information about specific vulnerability scans from Tenable.io. By automating the process of fetching scan details using a unique Scan ID, it streamlines vulnerability management and facilitates informed decision-making for security operations.

## Summary

The **Tenable.IO - Get Scan By ID** component automates the retrieval of scan details from Tenable.io based on a provided Scan ID. The workflow initiates by receiving the Scan ID as input and utilizes Tenable.io's API to fetch comprehensive information about the specified scan. The retrieved scan details are then published for use in subsequent processes or reporting. This automation ensures that security analysts have timely access to vital scan information, enhancing the effectiveness of vulnerability management and remediation efforts.

## Actions and Their Purpose

### Tenable Get Scan Details
**Type:** connector  
**Purpose:** Fetches detailed information about a specific vulnerability scan from Tenable.io using the provided Scan ID.

**On Success:**  
- **Calls:** Tenable_Scan_Status

**On Failure:**  
- No specific failure actions defined.

**Inputs:**
- path_parameters: 
  - scan_id: References the Scan_ID input provided by the user.

**Action:** tenable_io.get_scan_details

### Tenable Scan Status
**Type:** connector  
**Purpose:** Retrieves the current status of the launched vulnerability scan from Tenable.io to monitor its progress.

**On Success:**  
- No subsequent actions.

**On Failure:**  
- No specific failure actions defined.

**Inputs:**
- path_parameters: 
  - scan_id: References the Scan_ID input provided by the user.

**Action:** tenable_io.get_scan_status

### Update Result Variable
**Type:** updateVariables  
**Purpose:** Updates the component's output variables with the scan UUID, status, and progress obtained from Tenable.io.

**Inputs:**
- scan_uuid: References Tenable_Launch_Scan.result.json_body.scan_uuid
- status: References Tenable_Scan_Status.result.json_body.status
- progress: References Tenable_Scan_Status.result.json_body.progress

**On Success:**  
- The component’s execution concludes successfully.

## Process Flow Summary

1. **Initialization:** The component receives the Scan_ID as input, which uniquely identifies the vulnerability scan to be retrieved from Tenable.io.
2. **Scan Launch:** It initiates the retrieval of scan details by calling Tenable.io's get_scan_details API with the provided Scan_ID.
3. **Status Retrieval:** Upon successfully fetching the scan details, it retrieves the current status and progress of the scan using Tenable.io's get_scan_status API.
4. **Result Compilation:** The component compiles the scan UUID, status, and progress into the result variable.
5. **Finalization:** Updates the result variable with the compiled scan information, concluding the component successfully.
6. **Error Handling:** At any point of failure during the scan retrieval or status checking, the component ensures that errors are raised and recorded, maintaining the integrity and reliability of vulnerability management operations.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final scan details stored in the result variable.