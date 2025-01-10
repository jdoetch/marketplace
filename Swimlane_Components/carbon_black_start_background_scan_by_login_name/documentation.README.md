# Technical Documentation: Carbon Black - Start Background Scan by Login Name

## Overview

This document provides detailed technical information about the **Carbon Black - Start Background Scan by Login Name** component. This component is designed to assist security teams in initiating background scans based on the login name on devices managed through VMware Carbon Black Cloud. The component is crucial for organizations to ensure continuous security monitoring and managing the threat landscape effectively.

## Summary of the Component

The **Carbon Black - Start Background Scan by Login Name** component plays a vital role in proactive security measures, allowing admins to trigger scans without user intervention which ensures that devices are always in compliance with security policies and up-to-date against vulnerabilities.

## Actions Description

### Set Background Scan for Device

#### Purpose
This action connects with the VMware Carbon Black Cloud to set a background scan specifically targeting a device identified by a user's login name.

#### Steps
1. **Input Preparation**: Takes in login_username and constructs necessary JSON structures.
2. **Execution**: Calls vmware_carbon_black_cloud.set_background_scan_for_device using the aforementioned inputs.
3. **On-Success**: Triggers the update action that logs successful initiation.
4. **On-Failure**: Triggers the failure action that handles errors.

### Update
This step updates system variables to reflect the result of the initiated scan.

### Action Response
Generates variables based on the system's response which can be used for subsequent processes or logging.

### Failure Background Scan
Handles the process if the initiation of a background scan fails, setting appropriate response actions and error logging.

## Overall Process Flow

1. **Initiation**:
   - The component initiates via the 'Action Response' entry point, proceeding to check if the username pertaining to the login is available for scanning.

2. **Set Background Scan**:
   - Attempts to set a scan using the VMware Carbon Black Cloud connector.
   - On success, proceeds to update system variables.
   - On failure, records the error and triggers appropriate error handling mechanisms.

3. **Finalization**: 
   - Depending on the outcome, updates or logs are generated and published to ensure transparency and traceability of the scan activity.

This flow ensures that scans are initiated smoothly and any issues are handled promptly, maintaining the integrity and security of the device landscape.

## Conclusion

The **Carbon Black - Start Background Scan by Login Name** component is essential for maintaining an active posture in cybersecurity defenses, enabling automated scans that help identify and mitigate potential threats swiftly.

