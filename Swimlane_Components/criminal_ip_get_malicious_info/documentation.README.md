# Criminal IP - Get Malicious Info

## Overview
The "Criminal IP - Get Malicious Info" component is designed to assist security professionals and systems in identifying and understanding potential threats associated with specific IP addresses. Utilizing this component, users can automate the retrieval of malicious information linked with an IP address, enriching security protocols and enhancing threat intelligence capabilities.

## Component Summary
This technical documentation outlines the operations and workflow of the "Criminal IP - Get Malicious Info" component. Designed for integration with security systems, this component utilizes data from the vendor "Criminal", to provide detailed insights into the reputation and background of IP addresses.

## Actions Description
### Create Variables
- **Type:** createVariables
- **Purpose:** Initiates the component by setting up necessary variables.
- **On-Success:** Proceeds to make a request to fetch data.
- **On-Failure:** Not explicitly defined.

### Create Enrichment
- **Type:** transformation
- **Purpose:** Transforms the fetched data into a structured format, which includes details such as reputation type and timestamp.
- **On-Success:** Triggers the "Update Enrichment" action.
- **On-Failure:** Not explicitly defined.

### Update Enrichment
- **Type:** updateVariables
- **Purpose:** Updates the enrichment data with new information obtained from the Create Enrichment step.
- **On-Success:** Completes the component execution.
- **On-Failure:** Not explicitly defined.

### Request
- **Type:** HTTP
- **Purpose:** To fetch malicious information from the API endpoint "https://api.criminalip.io/v/feature/ip/malicious-info".
- **On-Success:** Initiates the Create Enrichment process.
- **On-Failure:** Triggers the "Normalize Create Error At WC" action.

### Normalize Create Error At WC
- **Type:** connector
- **Purpose:** Handles any potential errors from the Request action, ensuring that the failure is processed correctly and does not disrupt the overall flow.
- **On-Success:** Updates the enrichment process.
- **On-Failure:** Not explicitly defined.

## Overall Process Flow
1. **Initialization:** The component initiates by creating necessary variables.
2. **Data Request:** An HTTP request is made to fetch data from the specified endpoint.
3. **Error Handling:** Any errors in the request process are normalized.
4. **Data Transformation:** Incoming data is structured into a predefined format for further processing.
5. **Data Enrichment:** The transformed data is updated with additional insights.
6. **Completion:** The component concludes its execution after updating the enrichment data.

In conclusion, the "Criminal IP - Get Malicious Info" component automates the process of data retrieval and processing, providing valuable insights into potentially malicious IP addresses. This component significantly contributes to cyber security efforts by providing timely and accurate threat intelligence.

