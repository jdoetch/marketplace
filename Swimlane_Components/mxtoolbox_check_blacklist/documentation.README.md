# MxToolbox - Check BlackList Component Documentation

## Overview

The MxToolbox - Check BlackList component is an integral part of network security and email system management. It ensures that a system's IP or domain is not blacklisted, thereby helping maintain the integrity and reputation of the system. This document provides a detailed overview, action descriptions, and a flowchart summary of the MxToolbox - Check BlackList component.

## Summary of the Component

The MxToolbox - Check BlackList component facilitates the checking of IPs or domains against various blacklists to prevent potential blacklisting issues that could affect email deliverability and IP reputation. This is achieved through a series of predefined actions within the system, ensuring automated checks and responses based on the results gleaned from MxToolbox API.

### Process Flow Summary

1. **Initiation of Variable Creation**: The process begins by setting up necessary variables.
2. **HTTP Request to MxToolbox API**: An HTTP request checks the IP/domain blacklist status.
3. **Decision Making**:
   - If the check is successful, the process moves to data enrichment based on the API's response.
   - If the check fails, an error normalization process is triggered to manage and log errors appropriately.
4. **Outcome Handling**:
   - Success leads to further data enrichment actions.
   - Failure leads to an error logging and notification mechanism.

## Actions Described

### Create Variables

- **Type**: Variables Creation
- **Purpose**: Sets up necessary input and reference data for use in subsequent actions.
- **On success**: Proceeds to the blacklist check via the MxToolbox API.
- **On failure**: Ends the process, logs error.

### Toolbo Check BlackList

- **Type**: HTTP Request
- **Purpose**: Checks the blacklist status of a specified IP/domain.
- **Subsequent Steps**:
  - **On success**: Initiates data enrichment.
  - **On failure**: Normalizes error data for better error management and logs the error.

### Normalize GreatError ATWC

- **Type**: Error Handling Connector
- **Purpose**: Manages and normalizes the errors occurred during the blacklist check.
- **On success**: Updates enriched data.
- **On failure**: Logs error and ends process.

### Create Enrichment

- **Type**: Data Transformation
- **Purpose**: Enriches the blacklist check data by organizing and structuring it into a more usable format.
- **On success**: Updates the enriched data.
- **On failure**: Logs error.

### Update Enrichment

- **Type**: Variables Update
- **Purpose**: Updates the system with new enriched data.
- **On success**: Ends the process successfully.
- **On failure**: Logs error.

## Conclusion

The MxToolbox - Check BlackList component automates the checking of blacklist status using the MxToolbox API and manages responses based on the query result. This component helps in maintaining the reliability and reputation of your systems by ensuring they are not blacklisted.
