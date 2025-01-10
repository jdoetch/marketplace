# SSC - Create a Scorecard Tag

## Overview
The "SSC - Create a Scorecard Tag" component is designated to automate the creation of tags within a Security Scorecard platform. This allows users to systematically tag and categorize entities within their security posture assessments, enhancing both the visibility and management of security metrics.

## Summary of the Component
This component processes the creation of tags by interfacing with Security Scorecard's REST API. It handles different scenarios through a series of actions including variable creation, API requests, and data transformation to ensure the tag creation aligns with user-supplied input criteria.

## Detailed Process Flow

### Actions and Their Descriptions

1. **Create Variables**
   - **Type**: Create Variables
   - **Purpose**: Initializes necessary variables used throughout the tag creation process.
   - **On-Success**:
     - Proceed to create a request body formatted for API submission.
   - **On-Failure**: No subsequent steps defined.

2. **Create Request Body**
   - **Type**: Transformation
   - **Purpose**: Constructs the JSON body required for the API request based on user input.
   - **On-Success**:
     - Execute the API request to submit the newly created tag to the Security Scorecard platform.
   - **On-Failure**: No subsequent steps defined.

3. **Request**
   - **Type**: HTTP
   - **Purpose**: Submits the HTTP POST request to the Security Scorecard API to create a tag.
   - **On-Success**:
     - Trigger the "Create Enrichment" action if the request is successful.
   - **On-Failure**:
     - Proceed to the "Normalize Create Error" action to handle potential errors.

4. **Create Enrichment**
   - **Type**: Transformation
   - **Purpose**: Processes the response from the Security Scorecard API and prepares it for downstream actions or notifications.
   - **On-Success**:
     - Update enrichment details confirming the success of the operation.
   - **On-Failure**: No subsequent steps defined.

5. **Normalize Create Error**
   - **Type**: Connector
   - **Purpose**: Handles errors returned from the API request by normalizing and formatting them for error tracking and notification systems.
   - **On-Success**:
     - Updates the enrichment with normalized error data.
   - **On-Failure**: No subsequent steps defined.

6. **Update Enrichment**
   - **Type**: Update Variables
   - **Purpose**: Updates the enrichment details with either success confirmation or error details, completing the process.
   - **On-Success**: No subsequent steps defined.
   - **On-Failure**: No subsequent steps defined.

## Overall Process Flow Summary
The flow begins with creating necessary variables, followed by forming a request body suitable for the API. An HTTP request is then made to create the scorecard tag. Depending on the response, it either moves towards enrichment upon success or error normalization upon failure. The final step updates the enrichment data, which concludes the process of tagging within the Security Scorecard environment.

### Flow Diagram Reference
Please refer to the accompanying Mermaid diagram for a visual representation of this process.

