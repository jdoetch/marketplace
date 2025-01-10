# Criminal IP - Initiate Domain Scan Lite Component Documentation

## Overview
The "Criminal IP - Initiate Domain Scan Lite" component is designed for security automation, particularly focusing on the initiation of domain reputation scans through the Criminal IP API. This component automates the process of sending a domain scan request, processing the response, and handling errors or updates related to enrichment activities.

## Process Flow Summary
1. **Initiation**: The process begins by creating necessary variables for the operation.
2. **Domain Scan Request**: A HTTP request is crafted and sent to the Criminal IP API to initiate the domain scan.
3. **Response Handling**: Depending on the API's response, the flow either updates the enrichment or handles any errors that occurred during the request.
4. **Error Normalization**: If an error occurs, it is normalized using a dedicated connector.
5. **Final Enrichment Update**: After successfully processing the API's response or handling errors, the final enrichment data is updated and the process concludes.

## Detailed Actions
### Create Variables
- **Type**: Variable creation
- **Purpose**: Prepares necessary variables that will be used throughout the component.
- **On Success**: Proceeds to send the domain scan request.
- **On Failure**: Not applicable in the creation of variables.

### Request - Send Domain Scan Request
- **Type**: HTTP Request
- **Purpose**: Sends a domain scan request to the Criminal IP API.
- **On Success**: Triggers the "Create Enrichment" action to handle the API's response.
- **On Failure**: Activates the "Normalize Create Error" action to handle any issues encountered during the request.

### Create Enrichment
- **Type**: Transformation
- **Purpose**: Handles the API's response by creating enrichment data based on the response.
- **On Success**: Initiates the "Update Enrichment" action to finalize the enrichment process.
- **On Failure**: Typically, this would be where error handling specifics would be detailed.

### Update Enrichment
- **Type**: Variables Update
- **Purpose**: Updates the enrichment data with new or additional details obtained from the API's response or through transformation.
- **On Success**: Concludes the process if there are no errors.
- **On Failure**: This would involve further error handling mechanisms, depending on the specifics of the use case.

### Normalize Create Error
- **Type**: Connector
- **Purpose**: Normalizes and structures any errors encountered during the "Create Variables" or "Send Domain Scan Request" actions.
- **On Success**: Updates the enrichment data with error details.
- **On Failure**: Further error handling processes would be executed as necessary.

## Conclusion
This component, "Criminal IP - Initiate Domain Scan Lite," automates the initiation and handling of domain scan operations through the Criminal IP API. From variable preparation, request handling, error normalization to final enrichment updates, each action is structured to ensure seamless operational flow. This technical documentation helps users understand each component of the process, ensuring clarity and ease of use for security automation.
