# Censys ASM - Get Risk Events Component Documentation

## Overview
The "Censys ASM - Get Risk Events" component is designed to harness the capabilities of Censys ASM to retrieve and analyze risk events related to digital assets. This component automates the process of fetching and processing risk event data, simplifying security management tasks. It is orchestrated to run within the Swimlane Turbine framework employing specialized actions to ensure seamless data retrieval and manipulation.

## Component Summary
This component entails a series of orchestrated steps which utilize actions such as variable creation, data transformation, and HTTP requests to interact with the Censys application programming interface (API). By automating these processes, security analysts can more efficiently track, record, and respond to risk events.

### Workflow Description

#### Action: Create Variables
- **Type:** Variables Creation
- **Purpose:** Initializes necessary variables used across the component.
- **On Success:** Proceed to trigger an HTTP request.
- **On Failure:** Stops execution and logs error.

#### Action: Create Enrichment
- **Type:** Transformation
- **Purpose:** Prepares and organizes data fetched from the API for further processing.
- **On Success:** Moves to update enrichment variables.
- **On Failure:** Stops execution and logs error.

#### Action: Update Enrichment
- **Type:** Variables Update
- **Purpose:** Updates enrichment data with fresh output from the prior transformation action.
- **On Success:** N/A
- **On Failure:** Stops execution and logs error.

#### Action: HTTP Request
- **Type:** HTTP
- **Purpose:** To retrieve risk events from the Censys API.
- **On Success:** Executes the Create Enrichment action.
- **On Failure:** Executes normalization error handling.
  
#### Action: Normalize Create Error
- **Type:** Connector
- **Purpose:** Manages any exceptions or errors during the HTTP request.
- **On Success:** Return to update enrichment.
- **On Failure:** Stops execution and logs error.

## Process Flow Summary
The component starts by creating necessary variables for execution. It then performs a secure HTTP request to fetch risk events from the Censys API. Depending on the results of this request, either an enrichment creation or error normalization takes place. Successful creation of enrichment leads to updating the enrichment data store. The entire component is structured to handle success and errors gracefully, ensuring data integrity and system resilience.

### Notes:
- This component should run within allowed Swimlane environments.
- Error handling is robust, providing clear paths for retries and logging.

This process flow ensures streamlined processing of risk events, enhancing the security posture of organizations by utilizing Censys ASM efficiently.

