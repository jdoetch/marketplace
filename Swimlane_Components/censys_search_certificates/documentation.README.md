# Censys - Search Certificates Component

## Overview
The "Censys - Search Certificates" component is designed for use within automation platforms that handle cybersecurity and digital certificate analysis. This component leverages the Censys API to search and analyze SSL/TLS certificates, allowing users to extract and utilize detailed certificate information effectively. 

## Detailed Description and Process Flow

### Actions

#### 1. Create Variables
- **Type:** Variable Creation
- **Purpose:** Initializes necessary variables used across the component.
- **On Success:** Proceeds to encode the query.
- **On Failure:** Ends the execution.

#### 2. Encode Query
- **Type:** Transformation
- **Purpose:** Encodes the search query to ensure it is URL-friendly, especially important for HTTP request compatibility.
- **On Success:** Triggers the execution of the main search call.
- **On Failure:** Ends the execution.

#### 3. Execute Search
- **Type:** HTTP Request
- **Purpose:** Performs the actual API call to Censys to fetch certificate data based on the provided query.
- **On Success:** Proceeds to process the fetched data (Create Enrichment).
- **On Failure:** Attempts error normalization.

#### 4. Normalize Create Error
- **Type:** Connector
- **Purpose:** Handles any errors from the search process, normalizing output for error handling routines.
- **On Success:** Updates enrichment data.
- **On Failure:** Ends the execution.

#### 5. Create Enrichment
- **Type:** Transformation
- **Purpose:** Transforms the data received from the API into a structured format, making it ready for further processing or output.
- **On Success:** Updates enrichment data.
- **On Failure:** Ends the execution.

#### 6. Update Enrichment
- **Type:** Update Variables
- **Purpose:** Updates the variables holding enrichment data with new values.
- **On Success:** Ends the execution successfully.
- **On Failure:** Ends the execution with errors.

### Overall Process Flow
1. The component begins by creating necessary variables.
2. It then encodes the query for proper URL format.
3. With a properly formatted query, the component executes the API search.
4. Handling of any potential errors from the API request is performed.
5. If the data is received successfully, it is transformed into a structured enrichment format.
6. Finally, the enrichment data is updated for use in further steps or outputs.

## Benefits
Automating the process of searching and analyzing certificates with "Censys - Search Certificates" ensures high efficiency and accuracy in handling SSL/TLS certificates across the network. This benefits organizations by enhancing security and compliance with digital communication standards.

