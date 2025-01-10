# SSC - Get all Scorecard Tags Component Documentation

## Introduction
The SSC - Get all Scorecard Tags component is designed for automatic procurement of tags from Security Scorecard's API. This helps in the automation of security assessments and monitoring by fetching relevant scorecard tags that can be utilized for enhanced security analytics and decisions. This component facilitates the integration with Security Scorecard, streamlining data acquisition processes involved in security operations.

## Component Overview
"SSC - Get all Scorecard Tags" interacts with the Security Scorecard to retrieve a list of all scorecard tags. This interaction helps in categorizing and understanding the security posture of different entities monitored by the Security Scorecard platform.

### Action Summary
The component is structured around several key actions which together ensure the complete retrieval and handling of scorecard tags:
1. **Create Variables**
   - **Type**: CreateVariables
   - **Purpose**: Initializes necessary variables for processing.
   - **Flow**:
     - **On Success**: Proceed to Request action
     - **On Failure**: Ends the process

2. **Request**
   - **Type**: HTTP
   - **Purpose**: To make a HTTP request to the Security Scorecard API endpoint to fetch scorecard tags.
   - **Flow**:
     - **On Success**: Triggers Create Enrichment action
     - **On Failure**: Triggers Normalize Error action

3. **Create Enrichment**
   - **Type**: Transformation
   - **Purpose**: Transforms the fetched data into a structured format for further processing.
   - **Flow**:
     - **On Success**: Proceed to Update Enrichment action
     - **On Failure**: Ends the component

4. **Update Enrichment**
   - **Type**: UpdateVariables
   - **Purpose**: Updates the variables based on the newly transformed data.
   - **Flow**:
     - **On Success**: Ends successfully
     - **On Failure**: Ends the component

5. **Normalize Error**
   - **Type**: Connector
   - **Purpose**: Handles any errors encountered during the HTTP request.
   - **Flow**:
     - **On Success**: Retry Update Enrichment
     - **On Failure**: Ends the component

### Overall Process Flow Summary
1. Initialize variables necessary for the operation.
2. Execute an HTTP request to fetch the scorecard tags.
3. On successful fetch, transform the data into a more structured format.
4. Update the system with the transformed data.
5. If any step fails, handle the error and normalize the output for logging and retry mechanisms.

This ensures a comprehensive and error-resistant operation capable of integrating seamlessly with external API points provided by Security Scorecard, thus empowering security teams with automated tools for better efficiency.

