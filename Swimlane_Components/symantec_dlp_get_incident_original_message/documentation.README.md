# Symantec DLP - Get Incident Original Message

## Overview
The "Symantec DLP - Get Incident Original Message" component is designed to facilitate the retrieval of the initial communication details from incidents managed by Symantec's Data Loss Prevention (DLP) software. This component plays a crucial role in automating the process of data extraction, aiding in quicker response and detailed analysis of security incidents.

## Summary of the Component
The aim of this component is to provide a seamless integration with Symantec DLP to fetch the original message of any incident. This is particularly useful in environments where quick access to incident details is crucial for compliance and security response teams.

## Process Flow
1. **Initiation**: The process begins by receiving an incident ID which triggers the component.
2. **Action Execution**: The main action, `symantec_dlp.get_incident_original_message`, takes the incident ID, executes the retrieval process and handles different outcomes:
    - **On Success**: Proceed with data transformation.
    - **On Failure**: Terminate the process or handle exceptions.
    - **On Completion**: Consolidates results and prepares them for further usage or reporting.
3. **Result Transformation**: Transform and prepare the data for integration into other systems or for reporting purposes.

## Detailed Actions and Steps
### Get Incident Original Message (Action)
- **Type**: Connector
- **Purpose**: To retrieve the original message associated with an incident in Symantec DLP.
- **On-Success**: Moves to the result transformation stage.
- **On-Failure**: Logs the error or retries, based on predefined conditions.
- **Inputs Required**:
  - **Path Parameters**: Incident ID (a numerical identifier for the incident).
  - **Verify SSL**: A Boolean flag to verify SSL certificates, enhancing security.

### Component Result (Transformation)
- **Type**: Transformation
- **Purpose**: To transform the fetched data into a usable format or integrate it with other systems.
- **On-Success**: Data is published to the desired destination or used in subsequent processes.
- **On-Failure**: Error handling procedures are executed.
- **Processing Details**:
  - **Result Transformation**: Converts the raw data into a structured format, applying any necessary business logic or rules.

## Overall Process Flow Summary
The component starts by checking if the incident ID is provided, then uses the Symantec DLP connector to fetch the original incident message. Upon successful retrieval, the data undergoes transformation. Depending on the outcome, appropriate success or failure paths are followed, and the process is concluded by either publishing the result or handling it as configured.

This document intends to provide clear and detailed insights into the "Symantec DLP - Get Incident Original Message" component, ensuring that users can integrate and utilize this component effectively within their incident response framework.
