# Tenable VM - Get Template List - Technical Documentation

## Overview

This document covers the "Tenable VM - Get Template List" component, designed to facilitate the retrieval and management of template lists from Tenable VM, thereby enhancing vulnerability management processes.

### Purpose

The "Tenable VM - Get Template List" component exists to interact with the Tenable VM API to fetch a list of available templates, which can be utilized for configuring scans, policies, and remediations. This component forms a crucial part of security automation, allowing for seamless integration and efficient template management.

## Process Flow Summary

1. **Start:** Initialization of the component.
2. **Enable List Templates:** Requests Tenable VM to list all available templates.
3. **Extract Template Details:** Processes the returned list to extract detailed template information.
4. **Filter Templates:** Optionally filters the list based on specific criteria (like template title).
5. **End of Flow:** Outputs are either success or failure, leading to subsequent steps based either way. 

## Detailed Actions

### Enable List Templates

- **Type:** Connector
- **Purpose:** To initiate a connection with Tenable VM and list all available templates.
- **On-Success:**
  - **Extract Template Details:** Further processing of the fetched templates to gather more detailed information.
- **On-Failure:** Log error, trigger corrective actions or alerts.
  
### Extract Template Details

- **Type:** Transformation
- **Purpose:** Processes and transforms the template data into a structured format easy for further utilization.
- **Transformations:**
  - **Filtered Templates:** Extracts certain parts of templates based on specified conditions.
  - **Template Count:** Counts the number of templates filtered or returned in the initial fetch.
- **On-Completion:** Determines next actions based on data availability and condition checks.

## Environmental and Dependency Information

- **Assets Required:** enable_
- **Input Types:** This component can handle different types of templates such as "remediation," "policy," and "scan."
- **Security Configurations:** All data transformations and transmissions are secured under current best practices.

## Publishing Outputs

- **Templates:** List of templates from Tenable VM.
- **Filtered Templates Size:** Number of templates that meet the filter conditions.
- **Overall Templates Size:** Total count of templates fetched.

This component ensures organizations can automate part of their security operations, focusing on vulnerability management with updated and relevant template data from Tenable VM.

