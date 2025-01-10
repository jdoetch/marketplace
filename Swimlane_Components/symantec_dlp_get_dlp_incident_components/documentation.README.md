# Symantec DLP - Get DLP Incident Components Documentation

## Overview
The Symantec DLP - Get DLP Incident Components is designed to facilitate the retrieval of incident components from the Symantec Data Loss Prevention system. This document serves as technical documentation tailored for end users operating in environments with dark backgrounds and high contrast needs. Here you will find a comprehensive guide detailing the process flow, action descriptions, and an overall summary of the component.

## Component Purpose
The purpose of this component is to provide automated mechanisms to fetch components related to specific incidents recorded in Symantec's Data Loss Prevention system. This automation is critical in efficiently managing data security and compliance measures.

## Process Flow Summary
1. **Initiate Incident Components Retrieval**:
   - The component receives an incident ID and uses it to fetch the relevant DLP incident components.
   - This action is performed through a connector to Symantec DLP utilizing secure pathways (validated by SSL verification).

2. **Transformation of Data**:
   - Once data is retrieved, it undergoes a transformation to ensure it is in the correct format for further use or reporting.
   - This includes checking the presence of JSON bodies in responses and extracting necessary information.

3. **Completion Handling**:
   - Determines the final state of the request. If the retrieval and transformation are successful, it marks the operation as complete.
   - In case of errors, it handles failures gracefully by providing clear failure logs.

## Detailed Actions Description
### Retrieve Incident Components
- **Type**: Connector
- **Description**: Connects to Symantec DLP to retrieve details of a specific incident based on the incident ID provided.
- **On-Success**: Proceed to transform the retrieved data.
- **On-Failure**: Logs the error details.
- **Inputs**:
  - **Path Parameters**: Incident ID
  - **Verify SSL**: True, to ensure secure communication.

### Transform Retrieved Data
- **Type**: Transformation
- **Description**: Transforms and validates the JSON structure of the retrieved data.
- **On-Success**: Complete the component successfully.
- **On-Failure**: Record the failure details.
- **Transformations**:
  - Checks and extracts information from the JSON body.
  
## Conclusion
This component automates the retrieval and transformation of incident data within Symantec's DLP systems, enhancing data security operations and compliance reporting. The automation provided by Symantec DLP - Get DLP Incident Components eases the demand on security teams and accelerates incident response times.

