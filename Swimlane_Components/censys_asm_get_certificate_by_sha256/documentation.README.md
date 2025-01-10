# Censys ASM - Get a Certificate by SHA256

## Overview
The "Censys ASM - Get a Certificate by SHA256" component is designed to interact with the Censys API to retrieve certificate details by their SHA256 hash. This component streamlines the process of certificate validation and analysis in security operations, leveraging the comprehensive digital asset database provided by Censys.

## Purpose
The flow ensures efficient retrieval and processing of certificate details, critical in verifying certificate authenticity and understanding associated assets. The core feature is particularly relevant in environments where security and precision are paramount.

## Component Process and Actions Descriptions

### 1. Create Variables
This action initializes various operational variables needed throughout component execution.
- **Type**: Create Variables
- **Purpose**: Setup necessary variables for the operation.
- **On-Success**: Proceed to request action.
- **Inputs**: 
  - Enrichment Type, Enrichment Provider, etc.

### 2. HTTP Request
Executes an HTTP request to the Censys API using the shard SHA256.
- **Type**: HTTP
- **Purpose**: Retrieve certificate data from Censys.
- **On-Success**: Trigger "Create Enrichment".
- **On-Failure**: Trigger "Normalize Create Error at WC".
- **Inputs**:
  - Endpoint: HTTPS endpoint for Censys API.

### 3. Create Enrichment
Processes the data received from the HTTP request to structure the enrichment data.
- **Type**: Transformation
- **Purpose**: Structure the received data into a usable format for further actions.
- **On-Success**: Proceed to update enrichment action.
- **Inputs**: Result from HTTP Request.

### 4. Update Enrichment
Updates the enrichment data based on new or transformed input.
- **Type**: Update Variables
- **Purpose**: Ensure the enrichment data is current and accurate.
- **Inputs**: Result from "Create Enrichment".

### 5. Normalize Create Error at WC
Handles exceptions or errors encountered during the HTTP request phase.
- **Type**: Connector
- **Purpose**: Provide a standardized error handling mechanism.
- **On-Success**: Update enrichment with error details.
- **Inputs**: Error details from HTTP error response.

## Overall Process Flow
The overall process begins with setting up necessary variables, followed by an HTTP request to retrieve certificate data using its SHA256 identifier. Depending on the response, the component either processes the data received or handles possible errors. Success in initial stages leads to data enrichment actions, ensuring the data is prepared and formatted for end-user needs or subsequent system processes.

The final data output provides enriched, structured certificate information, making it actionable and meaningful for security analysis and decision-making processes.

