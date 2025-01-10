# Censys - Add Tag to Host Component Technical Documentation

## Overview
The "Censys - Add Tag to Host" component is designed for integrating with the Censys platform to enhance host records by adding tags. This component is utilized within automation environments to streamline the process of tagging host assets for better identification and categorization in security operations.

## Component Summary
The component operates by interfacing with the Censys API to append user-defined tags to specific hosts identified by their IP addresses or other identifying information. It forms part of a broader automation architecture where host data enrichment is a recurring requirement.

### Process Flow
1. **Create Variables**: Initializes variables required for the operation.
   - **Type**: Variable Creation
   - **On-Success**: Proceeds to send an HTTP request.
   - **On-Failure**: The workflow ends.

2. **HTTP Request (Request)**: Makes an HTTP request to the Censys API to add a tag to a host.
   - **Type**: HTTP Request
   - **On-Success**: Triggers the creation of enrichment data.
   - **On-Failure**: Triggers error normalization process.

3. **Create Enrichment**:
   - **Type**: Transformation
   - **Purpose**: To collect and transform data received from the HTTP request.
   - **On-Success**: Initiates the Enrichment Update.
   - **On-Failure**: The workflow ends.

4. **Update Enrichment**: Updates enrichment variables with new data.
   - **Type**: Variable Update
   - **On-Success**: Ends successfully.
   - **On-Failure**: Ends with an error.

5. **Normalize/Create Error Data**:
   - **Type**: Connector
   - **Purpose**: Handles and formats error data if the HTTP request fails.
   - **On-Success**: Re-attempts updating the enrichment data.
   - **On-Failure**: The workflow ends.

### Detailed Action Descriptions
- **Create Variables Action**:
  - Instantiates necessary variables for operation execution.
  - Inputs include definitions for types of enrichment and operational parameters.

- **HTTP Request Action**:
  - Responsible for communicating with the Censys API.
  - Configured to handle secure HTTP requests with verification and redirection handling.
  - Inputs specify the endpoint, method, headers, and query parameters.

- **Create Enrichment Action**:
  - Processes the response from the API to extract and structure necessary information.
  - Applies a JSON transformation to parse and store data effectively.

- **Normalize/Create Error Data Action**:
  - Activated upon failures in earlier actions, specifically the HTTP request.
  - Extracts error details and prepares them for logging or reprocessing.

## Overall Process Flow
The component's execution begins with setting up variables and then attempting to add a tag via the Censys API. Depending on the success or failure of the API call, it either progresses to data enrichment or error handling, ensuring robust processing and responsiveness to operational anomalies.

### Error Handling
Special attention is given to error handling, with specific actions designated to manage and normalize error outputs, thus maintaining the integrity and continuity of the automation process.

