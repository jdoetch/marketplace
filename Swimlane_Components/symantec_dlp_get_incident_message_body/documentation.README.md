# Symantec DLP - Get Incident Message Body: Technical Documentation

## Overview

The "Symantec DLP - Get Incident Message Body" component is a crucial automation within the data loss prevention framework provided by Symantec DLP solutions. It enables a streamlined approach to fetching the content of a message flagged as an incident, thus facilitating rapid response and analysis by security teams.

## Purpose

The primary objective of this component is to enhance the incident response process by automating the retrieval of message bodies from incidents detected by Symantec DLP. Automated retrieval speeds up the analysis process, helping security personnel to mitigate and resolve incidents more effectively.

## Actions Description

### Get Incident Message Body

- **Type:** Connector
- **Description:** Adds an asset and passes in an Incident ID to retrieve the message body from a Symantec DLP incident.
- **Inputs:** 
  - **ID:** Incident ID required to fetch the incident message.
  - **Verify SSL:** Ensures the security of the connection.
- **Outputs:** Retrieves the message content for the given incident ID.
- **On-success:** Continues to the next defined step if message retrieval is successful.
- **On-failure:** Actions to perform if the retrieval fails are predefined in the component setup.
- **On-complete:** Triggers the subsequent action called "Component Result".

### Component Result

- **Type:** Transformation
- **Description:** Handles the result data from the Get Incident Message Body action.
- **On-success:** Actions to process the transformed data.
- **On-failure:** Handles errors in the data transformation process.
- **On-complete:** Completes the action and optionally triggers additional processes.
- **Transformations:** Processes and maps the result data for use in subsequent actions.

## Process Flow Summary

1. **Initiation:** Triggered by an incident ID input.
2. **Action Execution:** The "Get Incident Message Body" action is executed, fetching the message body from Symantec DLP.
3. **Data Handling:** On successful execution, the result is passed to the "Component Result" for data transformation.
4. **Completion:** The entire process either resolves successfully with fetched and transformed data or handles failures at each step accordingly.

This component ensures that incident response teams have quicker access to incident details, critical for prompt and effective action.
