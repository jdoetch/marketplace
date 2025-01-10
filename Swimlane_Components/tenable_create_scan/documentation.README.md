# Tenable - Create Scan Component Documentation

## Introduction

The "Tenable - Create Scan" component is designed to automate the creation of scan tasks using Tenable's security platform. This component helps organizations streamline their security operations by programmatically setting up scans, defining target assets, and scheduling these scans according to operational requirements.

## Summary of the Component

The "Tenable - Create Scan" component includes several key actions focused on setting up and managing the lifecycle of scans within a security environment. The primary function is handled by the action enable_create_scan, which interacts with the Tenable.io platform to configure and initiate new scans.

## Detailed Actions Description

### enable_create_scan

#### Purpose
This action serves as the main entry point for creating scans in Tenable.io. It configures a new scan based on detailed input parameters, schedules the scan, and handles permissions.

#### Type
- **Type**: Connector
- **Action**: tenable_io.create_scan

#### Input Parameters
- **template**: Utilizes a template for the scan configuration.
- **scan_name**: Defines the name of the scan.
- **scan_enabled**: A boolean indicating whether the scan should be scheduled (enabled).
- **agent_group_id**: Specifies the agent groups that are targeted for the scan.
- **scan_time_window**: Sets the time window during which the scan must complete.
- **other scan_specific settings**: Includes ACLs, launch type, folder ID for storing the scan, tagging options, and more.

#### Process Flow
1. **On Success**: The scan result is published.
2. **On Failure**: Specific actions or notifications can be triggered.

#### Subsequent Steps
- **On Complete**: Actions to verify or manage the scan results.

## Overall Component Flow
1. The entry point of the component is initiated through the enable_create_scan action.
2. The user inputs required for starting a scan are gathered based on predefined schemas.
3. Upon successful creation of the scan, the result is published and can be used for further actions or audits.
4. In case of failures, the system can be set up to notify or trigger corrective workflows.

### Environment and Integration

This component requires an active Tenable.io connection configured in the system.

## Versioning and Schema Information
- **Version**: The component is kept up-to-date with the latest API changes from Tenable.
- **Schema Reference**: aec-ecb-f-c-ddcb

## Conclusion

This component automates the scan creation process in Tenable.io, enhancing security operations by efficient scan management, customizable scan templates, and integrated response actions.

