# Censys - Remove Tag from Host Component Documentation

## Overview

The "Censys - Remove Tag from Host" component is designed to facilitate the removal of tags from hosts within the Censys data landscape. This document outlines the technical functionalities, flow processes, actions, and interaction points of the component for effective utilization in an automated environment.

## Component Summary

This component primarily interacts with the Censys API to manage tags associated with specific hosts. It ensures that tags that are no longer relevant can be efficiently removed, thus keeping the tagging system up-to-date and relevant.

## Process Flow

1. **Start**
   - The process begins with the initiation of the component in the user's environment.
  
2. **Create Variables**
   - **Action:** Creates necessary variables for the process.
   - **On-success:** Proceeds to make a request to the Censys API.
   - **On-failure:** No further action, ends the process.

3. **Make API Request**
   - **Action:** Sends an HTTP request to remove a specific tag from a host in Censys.
   - **Type:** HTTP request.
   - **On-success:** Moves to create an enrichment based on the response.
   - **On-failure:** Normalizes error data.
   - **Endpoint details:** Constructed dynamically based on inputs for host and tag.

4. **Create Enrichment**
   - **Action:** Transforms the API response into a structured format.
   - **Type:** Transformation.
   - **On-success:** Updates the enrichment data.
   - **On-failure:** Ends the process.

5. **Update Enrichment**
   - **Action:** Updates the local data store with new enrichment data.
   - **Type:** Update variables.
   - **On-complete:** Completes the process.

6. **Normalize Error**
   - **Action:** Handles errors by structuring them into a predefined format.
   - **Type:** Connector.
   - **On-success:** Updates failure information in the enrichment data.

## Detailed Action Descriptions

### Create Variables
This initial action sets up necessary variables for the component's operations. It is essential for holding data that will be used in subsequent steps.

### Make API Request
This is a key action where an HTTP request is made to the Censys API. It uses dynamic variables such as host ID and tag to construct the request endpoint. The success of this action dictates the flow direction towards either enrichment creation or error normalization.

### Create Enrichment
Based on the successful API response, this action formats the received data into a structured enrichment format, making it ready for internal use or further processing.

### Update Enrichment
This action updates the system's internal data stores or variables with the newly created enrichment data, ensuring that all components within the environment have the latest information.

### Normalize Error
In the event of an API failure, this action restructures the error data into a uniform format, which simplifies error handling and logging.

## Conclusion

The "Censys - Remove Tag from Host" component is a crucial automation tool that interacts with Censys APIs to manage host tags efficiently. By following the described flow, users can integrate this component within their environment to ensure effective tag management and data enrichment processes.
