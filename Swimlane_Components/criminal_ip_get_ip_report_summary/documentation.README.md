# Criminal IP - Get IP Report Summary

## Overview

The "Criminal IP - Get IP Report Summary" component is designed to automate the process of retrieving summary reports for IP addresses from the Criminal IP database. This automation component helps in enhancing cybersecurity measures by providing quick access to IP reputation, which aids in the decision-making process regarding security threats.

## Component Actions

### Create Variables

- **Type:** Create Variables
- **Purpose:** Initializes the variables used within the component.
- **On Success:** Proceeds to the HTTP request action.
- **On Failure:** The flow terminates or moves to an error handling routine.

### HTTP Request

- **Type:** HTTP
- **Description:** Sends an HTTP request to the Criminal IP API to retrieve the IP report summary.
- **Inputs:**
  - **Endpoint:** `https://api.criminalip.io/v/asset/ip/report/summary`
  - **Query Parameters:** Includes the `ip` parameter to specify which IP report to retrieve.
- **On Success:** Triggers the "Create Enrichment" action.
- **On Failure:** Moves to the "Normalize Create Error" action.

### Create Enrichment

- **Type:** Transformation
- **Purpose:** Processes the data received from the HTTP request to structure the enrichment data.
- **On Success:** Updates the enrichment data.
- **On Failure:** The flow may terminate or handle the error accordingly.

### Update Enrichment

- **Type:** Update Variables
- **Purpose:** Updates the enrichment variables with processed data.
- **On Success:** Typically ends the successful execution of the component.
- **On Failure:** Error handling routines are initiated.

### Normalize Create Error

- **Type:** Connector
- **Description:** Handles errors from the HTTP request, normalizing them for consistent error management.
- **On Success:** Goes back to update enrichment action with the error context.
- **On Failure:** Ends or moves to global error handling.

## Process Flow Summary

1. **Initialization:** The component begins by creating necessary variables.
2. **Data Retrieval:** An HTTP request is made to fetch the IP report summary.
3. **Data Processing:** If the request is successful, the data is transformed into a structured format.
4. **Data Update:** After processing, the enriched data is updated.
5. **Error Handling:** In case of any failures during the HTTP request, errors are normalized and processed accordingly.

This systematic approach ensures that every IP report retrieval is handled efficiently, feeding valuable data into security systems and enhancing overall cybersecurity responsiveness.

