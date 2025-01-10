# Cortex - Quarantine Endpoint Component Documentation

## Introduction
The Cortex - Quarantine Endpoint component is an integral part of cybersecurity automation tailored to effectively manage endpoint security through isolation and status management. This component is designed to assess, trigger, and execute endpoint quarantine actions based on predefined conditions, enhancing an organization’s ability to respond to potential threats swiftly and efficiently.

## Overview of Cortex - Quarantine Endpoint
The Cortex - Quarantine Endpoint component executes several actions associated with the isolation and status update of endpoints within a network, leveraging the Palo Alto Cortex platform. Its main goal is to prevent the spread of threats and ensure network integrity by isolating affected or potentially compromised endpoints.

### Action Descriptions

#### Find Endpoint by Name
- **Type**: Connector
- **Description**: This action queries for an endpoint by its hostname.
- **On-Success**:
  - **Endpoint Found**: Initiates the quarantine or unisolation process if conditions are met.
- **On-Failure**:
  - **Create Status (All Failed)**: Logs and publishes a failed status update.

#### Quarantine Rule
- **Type**: Conditional
- **Description**: Determines if the endpoint meets the conditions for quarantine based on the endpoint search results.
- **On-Success**:
  - Executes the isolation command.
- **Else**:
  - **Create Status (Endpoint Not Found)**: Logs status when no endpoint is found matching the criteria.

#### Isolate Endpoint
- **Type**: Connector
- **Description**: Applies the isolation command to the endpoint identified.
- **On-Success**:
  - **Create Status (Success - Endpoint Isolated)**: Updates and publishes the successful isolation status.
- **On-Failure**:
  - **Create Status (Error - Isolate All Failed)**: Logs and updates failure status if isolation fails.

#### Update Results
- **Type**: Update Variables
- **Description**: Updates the result variables based on the outcome of the isolation or unisolation action, to be used in subsequent status publications or logs.

### Process Flow Description
1. **Start**: Initiation of the sequence when an endpoint name and action (quarantine or cancel quarantine) is provided by the user or system.
2. **Find Endpoint by Name**: Search for an endpoint based on the hostname.
3. **Evaluating Quarantine Conditions**: Determine if the search results fulfill quarantine requirements.
4. **Action Execution**:
   - If quarantining: Attempt to isolate the endpoint.
   - Else if canceling quarantine: Attempt to unisolate the endpoint.
5. **Status Update**: Based on the action's success or failure, update and publish the status.
6. **End**: The process flow completes after updating the status.

## Summary
The Cortex - Quarantine Endpoint component automates critical steps involved in managing the security of network endpoints. By automating these processes, it significantly reduces the response time and manual overhead associated with such tasks, ensuring more rapid and consistent application of security measures across affected systems.

