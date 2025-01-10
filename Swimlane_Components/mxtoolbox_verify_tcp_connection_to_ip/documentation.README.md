# MxToolbox - Verify TCP Connection to an IP

## Overview
The **MxToolbox - Verify TCP Connection to an IP** component is designed to automatically verify the connectivity over TCP to a specified IP address. This document provides technical details and usage guidance to assist end users in integrating and utilizing this component effectively in their network monitoring or diagnostic tasks.

## Summary of the Component
This component performs a series of automated actions to check the connection stability and response from an IP address using the TCP protocol. It utilizes a sequential flow involving variable creation, enrichment processes, and error adjustments to handle success and failure cases aptly.

## Actions and Flows

### Create Variables
- **Type**: Creation of Necessary Variables
- **Purpose**: Initializes required variables to execute the connection check.
- **On-Success**: Proceeds to verify TCP connection.
- **On-Failure**: Error handling procedures are initiated.

### Verify TCP Connection
- **Type**: HTTP Connection Test
- **Purpose**: Establishes a TCP connection to the specified IP to verify connectivity.
- **Inputs**: Includes the target IP address and required TCP settings.
- **On-Success**: Leads to the creation of an enrichment record.
- **On-Failure**: Triggers error normalization processes.

### Create Enrichment
- **Type**: Data Enrichment
- **Purpose**: Enhances the gathered data upon a successful TCP check with additional contextual information.
- **On-Success**: Updates the enrichment data accordingly.
- **On-Failure**: No specific workflow, generally leads back to error handling.

### Update Enrichment
- **Type**: Update Variables
- **Purpose**: Updates the enrichment variables with the new or modified data post TCP connection verification.
- **Inputs**: References the results from Create Enrichment action.

### Normalize Error
- **Type**: Error Handling
- **Purpose**: Normalizes the error data for consistency across different executions and eases troubleshooting.
- **Inputs**: Ingests error specifics from the Verify TCP Connection failure.
- **On-Success**: Updates enrichment with normalized error data.

## Overall Process Flow
1. **Initialize**: Creation of necessary variables.
2. **Execute**: Verification of TCP connection.
3. **Enrich**: On connection success, enrich data; on failure, proceed to error normalization.
4. **Update/Handle Error**: Depending on the outcome, update the enrichment data or normalize errors.
5. **Complete**: Finalize the process, recording success or failure along with enriched or normalized outputs.

By adhering to this process, the **MxToolbox - Verify TCP Connection to an IP** component offers a robust tool for network administrators to monitor and diagnose connectivity issues efficiently.

