# Censys - Delete Comment on Certificate Component Documentation

## Overview
The "Censys - Delete Comment on Certificate" component is designed to facilitate the automated management of comments associated with digital certificates in the Censys database. This documentation outlines the component’s actions and their flow, providing end users with guidance on how the process operates.

## Component Summary
The component integrates with the Censys API to delete a particular comment from a specified certificate. Actions within the component determine the sequence of operations required to perform this task effectively, handle potential errors, and ensure data consistency.

## Detailed Action Description
Here's a detailed breakdown of each action within the component:

### 1. Create Variables
- **Type:** Variables Creation
- **Purpose:** Initialize and prepare variables used across the component.
- **Subsequent Steps:** Proceeds with an API request action on success.

### 2. API Request
- **Type:** HTTP Request
- **Purpose:** Calls the Censys API to delete a comment linked to a certificate using the specified endpoint with method DELETE.
- **On-Success:** Triggers the Create Enrichment action.
- **On-Failure:** Triggers the Normalize Great Error Network Connector.

### 3. Create Enrichment
- **Type:** Transformation
- **Purpose:** Processes the response from the API request to manage data effectively.
- **On-Success:** Executes the Update Enrichment action.

### 4. Update Enrichment
- **Type:** Variables Update
- **Purpose:** Updates the variable enrichment based on data received from the Create Enrichment action.
- **On-Success:** Completes the enrichment process.

### 5. Normalize Great Error Network Connector (normalize_great_error_network)
- **Type:** Connector
- **Purpose:** Processes and maps error data received from the API request in case of a failure.
- **On-Success:** Calls the Update Enrichment action to handle error data appropriately.

## Process Flow Summary
Here is the sequential flow of the "Censys - Delete Comment on Certificate" component:

1. Initialization of variables.
2. API request to delete the comment.
3. On success of the API call, create data enrichment from the API response.
4. Update enrichment data variables for further processing.
5. In case of an API request failure, normalize and process the error using a specialized error handling connector.
6. Update enrichment with the processed error information.

This component ensures seamless automation in managing certificate comments on the Censys platform, streamlining operations and reducing manual overhead.

