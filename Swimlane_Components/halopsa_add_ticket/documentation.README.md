# HaloPSA - Add Ticket
## Overview
The HaloPSA - Add Ticket component is part of a technical solution that allows IT and support teams to automate the creation of support tickets in the HaloPSA platform. This workflow is crucial for ensuring a systematic, fast, and accurate method of ticket creation, contributing to more efficient issue resolution and tracking. This document details the various actions, methods, and flow of information throughout the component.

## Description of the Flow
### Add Ticket Action
This action is the initial step in the component where an asset is added, and it carries the required input parameters that HaloPSA needs to create a new ticket. Here are the steps and functionality involved:

- **Type**: Connector
- **Purpose**: To submit all necessary data to the HaloPSA system to generate a new support ticket.
- **Inputs**:
  - `json_body`: Contains all ticket-related information such as date occurred, summary, status ID, details, etc.
- **On-Complete**:
  - Proceeds to `Component Result` action if successful.
- **Details**:
  - This is the main action point where data input into the HaloPSA system occurs. Additional inputs can be dynamically added under the 'Body, Object (Array)' section.

### Component Result Action
A transformation type action that handles the response from the HaloPSA ticket creation operation. The steps include:

- **Type**: Transformation
- **Purpose**: To handle and transform the ticket creation response.
- **Process**:
  - Checks if the `Create Ticket` action was successful and processes the JSON body of the result.
- **Outcomes**:
  - If `Create Ticket` is successful, no further actions are required.
  - In case of failure, appropriate failure handling mechanisms are triggered.

## Overall Process Flow
1. **Start**: Initiation of the ticket creation process.
2. **Add Ticket**: Submits data to HaloPSA.
3. **Check Result**: Determines the outcome of the 'Add Ticket' action.
4. **End Process**: Concludes the workflow based on the result of the ticket submission.

This component is essential for any IT support environment looking to leverage automation for effective and timely support management within the HaloPSA ecosystem.
