# Carbon Black - Isolate or Rejoin Device by ID

## Overview
The "Carbon Black - Isolate or Rejoin Device by ID" component enables users to manage the network connectivity of devices using VMware Carbon Black Cloud. Through specific actions, devices can be either isolated from or rejoined to a network, based on ID parameters provided. This technical documentation elucidates the functionality and systematic workflows built into the component, catering to the specific needs of security operations.

## Component Summary
This component is designed to facilitate the control of device connectivity via VMware Carbon Black Cloud. On triggering, the component assesses whether a given device identified by its ID should be isolated from or rejoined to the network, leveraging VMware’s capabilities. It is geared toward improving incident response efficiency and minimizing potential threats rapidly.

## Actions and Workflow Details
### Actions
1. **Isolate Device:** 
   - **Type:** Connector Action
   - **Purpose:** Disconnects a device from the network to prevent potential threat escalation.
   - **Subsequent Steps:**
     - On success: Registers a successful isolation response.
     - On failure: Logs the failure and provides feedback for review.

2. **Rejoin Device:**
   - **Type:** Connector Action
   - **Purpose:** Reconnects a device to the network once it is deemed safe.
   - **Subsequent Steps:**
     - On success: Registers a successful reconnection response.
     - On failure: Logs the failure and provides feedback for review.

3. **Handle Responses:**
   - **Type:** Update Variables
   - **Purpose:** To create or modify response messages based on the outcomes of the isolation or rejoining actions.

### Workflow Description
Upon initiation, the component first checks the required input for action type (isolate or rejoin) and device identification. Depending on the action specified:
- If 'isolate', the isolation protocol is run, followed by a success or failure response based on the outcome.
- If 'rejoin', the rejoining protocol is executed likewise. 

All responses are logged and handled through updating a dedicated variable, which records either the success or failure message.

## Process Flow Summary
1. **Receive Device ID and Action Type:** The workflow starts by receiving the device ID and whether to isolate or rejoin the device.
2. **Execute Action:** Based on the action type, the appropriate VMware connector is triggered to isolate or rejoin the device.
3. **Handle Outcome:** Depending on the action's success or failure, a corresponding variable is updated with the result.
4. **Complete Workflow:** After updating the response variable, the workflow concludes.

This component is key for operational agility, enabling rapid responses to threats detected in the environment managed by VMware Carbon Black Cloud.

