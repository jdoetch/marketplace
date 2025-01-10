# Symantec DLP - Get Static Incident Details Component Documentation

## Overview
The Symantec DLP - Get Static Incident Details component is designed for the retrieval of static details about incidents managed by Symantec's Data Loss Prevention (DLP) software. This component is vital for organizations looking to automate their incident response processes and quickly gather pertinent details without manual intervention, thereby enhancing security operations.

## Summary of the Component
The "Symantec DLP - Get Static Incident Details" component is structured to interface with Symantec DLP via predefined connectors. It accepts an incident ID as input and retrieves detailed information about the specified incident. This helps in promptly assessing the scope and specifics of an incident which is crucial for effective and swift incident management.

### Component Actions
#### Get Static Incident Details
- **Type:** Connector
- **Description:** Gathers static details about an incident from Symantec DLP.
- **Inputs:** 
  - `incident_id` (required): The ID of the incident to retrieve details for.
- **On Success:** If details are successfully retrieved, the process moves to the component result phase.
- **On Failure:** There are contingencies in place to handle failures in data retrieval.
- **Environment:** Uses default pool settings.

### Subsequent Steps
- **On-Complete:** Data gathered by the initial action is processed and transformed in the component result.

#### Component Result
- **Type:** Transformation
- **Description:** Processes and formats the incident details retrieved by the initial action.
- **Transformations:** 
  - Formats the JSON body of the result to ensure compatibility and readability across platforms.
- **On-Complete:** Data is prepared for publishing if necessary.

## Overall Process Flow
1. **Initiation:** Triggered by the need to retrieve incident details.
2. **Action Execution:** Performs the action to gather details from Symantec's API.
3. **Data Handling:** On successful retrieval, data is handed off for transformation.
4. **Completion:** The transformed data is then outputted or published as needed, marking the end of the component's workflow.

By automating this process, organizations can ensure faster incident response times and more accurate security assessments.

