# Censys ASM - Rescan Risk Instance Documentation

## Overview
The "Censys ASM - Rescan Risk Instance" component is designed to automate interactions with the Censys ASM platform to dynamically scan for risk instances. This component harnesses various actions to maintain and update the security status of digital assets by re-evaluating identified risks and ensuring that appropriate responses are applied through automation.

## Process Flow Summary
The flow initiates with the **_Request** action which calls Censys ASM's API to rescan a risk instance. Depending on the outcome of this initial request, if successful, it triggers the **Create Enrichment** action; if failed, it triggers the **Normalize Create Error** action.

1. **Create Variables**: Initializes necessary variables for processing.
   - **Type:** Create Variables
   - **Purpose:** Setup for downstream action inputs.
   - **Next Steps:** Proceeds to _Request on success.

2. **_Request**: HTTPS Request to Censys ASM API.
   - **Type:** HTTP Connector
   - **Purpose:** Initiate a rescan in the Censys ASM system.
   - **On-Success:** Triggers Create Enrichment.
   - **On-Failure:** Triggers Normalize Create Error.
   
3. **Normalize Create Error**: Processes error data.
   - **Type:** Connector
   - **Purpose:** Standardizes the error output for further diagnosis.
   - **Subsequent Step:** Update Enrichment is triggered regardless of the result.

4. **Create Enrichment**:
   - **Type:** Transformation
   - **Purpose:** Transforms the response data into an enriched format.
   - **On-Success:** Leads to Update Enrichment.
   
5. **Update Enrichment**:
   - **Type:** Update Variables
   - **Purpose:** Refreshes the enrichment variables with new data.
   - **Next Steps:** Ends the flow unless triggered again by Normalize Create Error.

## Detailed Description of Actions

### Create Variables
This component begins by setting up variables essential for the operation of subsequent actions. This involves no direct interaction with external systems but prepares the environment for a successful API call.

### HTTP Request (_Request)
This HTTP request action is critical as it reaches out to the Censys ASM API to initiate a rescan of a risk instance. The URL and headers are prepared according to Censys API requirements, focusing on rescan functionality. Success or failure of this action dictates the flow's direction.

### Normalize Create Error
In cases where the _Request action fails, this action takes over to normalize and log the error details. It adjusts error data into a standard format, making it easier for troubleshooting and consistent error handling across different components.

### Create Enrichment
Following a successful rescan request, the received data undergoes transformation. This action converts raw API response data into an enriched format that's more useful for downstream actions or logging purposes.

### Update Enrichment
Finally, the Update Enrichment action updates the system's understanding of an asset's risk profile based on the latest scan results. This keeps the system's risk assessments up to date and ensures appropriate response measures are executed based on current data.

## Conclusion
This technical document covers the **Censys ASM - Rescan Risk Instance** component, outlining its utility in integrating Censys ASM's dynamic risk reassessment capabilities with automated systems. Each action is purposed towards maintaining updated and accurate risk evaluations, thus aiding in proactive security management.
