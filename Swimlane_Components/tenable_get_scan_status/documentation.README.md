# Tenable - Scan Status Retrieval Component

## Short Description
This component retrieves the status and progress of a specified scan from Tenable.io, enabling users to monitor ongoing security scans efficiently.

## Overview
The Tenable - Scan Status Retrieval Component integrates with Tenable.io to fetch the status of a scan based on its ID. This component ensures seamless communication between your automation platform and Tenable.io, offering real-time updates on scan progress and completion.

### Purpose of the Component
The component serves as a crucial part of security automation by:
- Allowing users to track scan progress.
- Enabling decision-making based on scan status.
- Supporting broader workflows for vulnerability management.

## Summary of the Component
This component involves a single key action, Tenable_Get_Scan_Status, which queries the Tenable.io API for the status of a specific scan. The scan is identified using a Scan_ID provided as an input.

### Inputs
The component requires the following input:
- **Scan_ID (string)**: The unique identifier of the scan for which the status is to be retrieved.

### Outputs
The component publishes the following information:
- **status**: The current status of the scan (e.g., "running," "completed," etc.).
- **progress**: The percentage of the scan completed.

## Detailed Action Descriptions

### Action: Tenable_Get_Scan_Status

**Type:** Connector

**Purpose:**
This action connects to Tenable.io to retrieve the status and progress of a specified scan.

#### Action Details:
- **Inputs:**
  - **path_parameters:**
    - **scan_id**: Dynamically references the Scan_ID input provided by the user.
- **Action:** tenable_io.get_scan_status
- **Pool:** $default
- **Asset:** Tenable_io
- **Test Inputs:** A test input is provided with a sample scan_id of 372.

#### On-Success:
No subsequent actions are defined for success, allowing users to process the published data directly.

#### On-Failure:
No specific failure handling is configured, requiring external error management if necessary.

#### On-Complete:
No post-completion steps are defined, simplifying the component for single-purpose execution.

## Process Flow Summary
1. **Input Specification:**
   - The user provides a Scan_ID input.
2. **Action Execution:**
   - The Tenable_Get_Scan_Status action sends a request to Tenable.io, using the provided Scan_ID to retrieve scan details.
3. **Data Retrieval:**
   - Tenable.io responds with the scan status and progress.
4. **Data Publication:**
   - The component publishes the status and progress outputs for downstream use.
