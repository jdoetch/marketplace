# Criminal IP - Check if Hosting Component Documentation

## Overview
The "Criminal IP - Check if Hosting" component is designed to automate security checks by interrogating the IP information through the Criminal IP database. It uses an orchestrated sequence of actions to determine if a given IP is associated with any hosting services known for harboring malicious activities. This component plays an essential role in enhancing security measures by providing quick responses based on IP reputation and associated data.

## Summary of the Component
The Criminal IP - Check if Hosting component integrates with various actions and utilizes data transformation and conditional logic to ensure accurate fetch and analysis of IP-related data. This component interacts through specified input and output schemas, facilitating a systematic procession of enrichment data.

### Actions Description

1. **Create Variables**
   - **Type:** Create Variables
   - **Purpose:** Initiates the component by setting up necessary variables for IP information processing.
   - **On Success:** Triggers the IP hosting request.
   - **On Failure:** Defined actions on failure are not specified in the YAML data.

2. **IP Request**
   - **Type:** HTTP Request
   - **Purpose:** Performs an HTTP request to the Criminal IP API to check if the provided IP is associated with hosting services.
   - **On Success:** Initiates the 'Create Enrichment' action if the IP is associated with hosting services.
   - **On Failure:** Triggers 'Normalize Great Error at WC' to handle errors and normalize response details.

3. **Create Enrichment**
   - **Type:** Transformation
   - **Purpose:** Processes the received IP data to create an enrichment detail that identifies the hosting status.
   - **On Success:** Proceeds to 'Update Enrichment' action which updates the enrichment details based on new data.
   - **On Failure:** Defined actions on failure are not specified in the YAML data.
   
4. **Update Enrichment**
   - **Type:** Update Variables
   - **Purpose:** Updates the enrichment variables based on the new data processed in the 'Create Enrichment' step.
   - **On Success:** Leads back to the IP Request for further processing if necessary.
   - **On Failure:** Defined actions on failure are not specified in the YAML data.

5. **Normalize Great Error at WC**
   - **Type:** Connector
   - **Purpose:** Normalizes the errors occurred during the HTTP request process, ensuring that all errors are standardized.
   - **On Success:** Leads back to 'Update Enrichment' for corrective actions.
   - **On Failure:** Defined actions on failure are not specified in the YAML data.

## Overall Process Flow Summary
The component initiates by creating necessary variables followed by an IP request action to check hosting status. Upon success, it transforms the received data into a structured format which is then used to update enrichment details. In case of an HTTP request failure, it normalizes the error and re-initiates the enrichment update process. This cyclical process ensures continuous and accurate updates based on real-time IP analysis data.

This flow ensures the security operations are seamless, providing critical hosting status information that assists in threat intelligence and risk assessment activities.
