# Censys ASM - Get comments from a SubDomain

## Short Description
The "Censys ASM - Get comments from a SubDomain" component is designed to retrieve comments associated with subdomains as part of cyber security asset management. By integrating this component into workflows, security teams can automate the process of gathering valuable feedback and annotations made for subdomains, which is crucial for comprehensive domain monitoring and security analytics.

## Overview of the Component
This component uses a series of actions within an automated workflow to extract comments. These actions involve API requests to Censys, data transformations, error handling, and enrichment updates which aim at streamlining the process and ensuring data accuracy.

### Process Flow
1. **API Request to Censys:**
   - Initiates a GET request to Censys's API to fetch comments for a specified subdomain.
   - On success, triggers the enrichment creation action.
   - On failure, triggers the error normalization action.

2. **Create Enrichment:**
   - Processes the successful API response to format and extract relevant data.
   - On complete, updates the enrichment data.

3. **Update Enrichment:**
   - Updates the existing enrichment data based on the new data retrieved from the API response.

4. **Normalize and Handle API Errors:**
   - In case of API failure, this action formats error responses to standardize the output across different types of errors.
   - On completion, possibly triggers another attempt or logs the error appropriately.

### Action Details
- **API Request (HTTP Request)**
  - Type: HTTP
  - Purpose: Fetch comments from Censys's API endpoint for specified subdomains.
  - On-Success: Triggers the "Create Enrichment" action.
  - On-Failure: Triggers "Normalize and Handle API Errors" action.

- **Create Enrichment (Data Transformation)**
  - Type: Transformation
  - Purpose: Formats the data retrieved from the API response and prepares it for enrichment.
  - On-Success: Triggers "Update Enrichment" action.

- **Update Enrichment (Update Variables)**
  - Type: Update Variables
  - Purpose: To update the existing enrichment data with new information.

- **Normalize and Handle API Errors (Connector)**
  - Type: Connector
  - Purpose: Standardizes error responses for consistent error handling across the component.
  - On-Success: Continuation or completion of the process flow depending on the scenario.

## Overall Process Flow Summary
The component orchestrates a sequential flow wherein an initial request to fetch comments if successful, leads to data processing and updating the enrichment, and if unsuccessful, leads to error handling. This ensures a robust solution that handles both expected and unexpected scenarios efficiently, maintaining the integrity and accuracy of the data management process.
