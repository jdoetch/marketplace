# SSC - Create an IP Domain Tag Group

## Overview
The SSC - Create an IP Domain Tag Group component is designed to automate the process of tagging IP domains within a security environment. This process is crucial for organizations to manage and monitor their internet-facing assets effectively, ensuring that security measures are appropriately applied and maintained.

## Component Summary
This component automates the creation of IP domain tags, allowing for dynamic updates and management of domain categorizations based on security needs. The component comprises several actions, each with specific functionalities that ensure the efficient processing of IP domain data.

### Actions
#### Create Variables
- **Type:** Variable Creation
- **Purpose:** Initializes the necessary variables used throughout the component.
- **Steps:**
  - **On-success:** Proceed to create the request body.
  - **On-failure:** There are no specific failure steps defined.

#### Create Request Body
- **Type:** Transformation
- **Purpose:** Constructs the request body required for the API call to tag IP domains.
- **Steps:**
  - **On-success:** Make the HTTP request using the constructed body.
  - **On-failure:** No specific failure steps defined.

#### Request
- **Type:** HTTP Request
- **Purpose:** Performs the API call to the IP domain tagging service.
- **Steps:**
  - **On-success:** Trigger the Create Enrichment action.
  - **On-failure:** Triggers the Normalize Great Error action if the API call fails.

#### Normalize Great Error
- **Type:** Connector
- **Purpose:** Handles any errors returned by the API, ensuring that the component can gracefully handle and log issues.
- **Steps:**
  - **On-success:** Continues to update enrichment data.
  - **On-failure:** No specific failure steps defined.

#### Create Enrichment
- **Type:** Transformation
- **Purpose:** Processes the successful response from the IP domain tagging API to enrich the internal data.
- **Steps:**
  - **On-success:** Updates enrichment for further processing.
  - **On-failure:** No specific failure steps defined.

#### Update Enrichment
- **Type:** Update Variables
- **Purpose:** Updates the internal enrichment variables with new data processed in the Create Enrichment step.
- **Steps:**
  - **On-success:** This is typically the end of the component’s action unless further actions are specified.
  - **On-failure:** No specific failure steps defined.

## Process Flow
1. **Initialization**: Create necessary variables.
2. **Data Preparation**: Build the request body for tagging.
3. **Execution**: Make the HTTP request to the tagging service.
4. **Error Handling**: Normalize any errors encountered during the HTTP request.
5. **Data Enrichment**: Process the response from the service and update enrichment data.
6. **Finalization**: Complete the update of enrichment data.

This automation component plays a vital role in maintaining the security and organization of IP domains by efficiently tagging them in a scalable manner.

