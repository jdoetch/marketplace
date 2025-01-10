# Censys ASM - Delete Tag from a Web Entity: Technical Documentation

## Overview
This document serves as technical documentation for the component "Censys ASM - Delete Tag from a Web Entity." It provides a comprehensive overview of the component's actions, purposes, and process flow, specifically aimed at technical end users who will interact with this system. The documentation is designed to offer high-contrast visibility to ensure accessibility on dark background interfaces.

## Component Summary
The "Censys ASM - Delete Tag from a Web Entity" component is crafted to manage and remove specific tags from web entities listed within the Censys ASM platform via the API. This functionality is essential for maintaining the accuracy and relevance of tagged data within enterprise applications.

### Process Flow
1. **Encode Identifier**
   - **Type:** Transformation
   - **Purpose:** Converts the identifier into a suitable format for further actions.
   - **On Success:** Proceed to send an HTTP request with the encoded identifier.
   - **On Failure:** End the process.

2. **Send HTTP Request**
   - **Type:** HTTP
   - **Purpose:** Interacts with the Censys ASM API to delete a tag from a web entity.
   - **On Success:** Invoke the creation of enrichment data.
   - **On Failure:** Normalize error and output the error data.

3. **Create Enrichment**
   - **Type:** Transformation
   - **Purpose:** Processes the results from the HTTP request for additional data manipulation or enrichment.
   - **On Success:** Update the enrichment information.
   - **On Failure:** End the process, log this action for audit purposes.

4. **Update Enrichment**
   - **Type:** Variables Update
   - **Purpose:** Updates or sets the values based on newly created enrichment.
   - **On Success:** Successfully completes the update.
   - **On Failure:** Log or handle error depending on system setup.

5. **Normalize and Output Error Data**
   - **Type:** Connector
   - **Purpose:** Captures and logs error data if the HTTP request to delete the tag fails.
   - **On Success:** Inform the user of failure and provide error specifics.
   - **On Failure:** End the process, ensure error logging is in place.

### Additional Component Information
- **Meta Data and Version Control:** The component includes version control and auditing features enabling tracking of modifications and usage by specific operators.
- **Error Handling:** The component contains robust error handling and normalization methods to ensure that operations staff can quickly address and troubleshoot any issues that arise during its operation.

## Conclusion
This document detailed the "Censys ASM - Delete Tag from a Web Entity" component's purpose, actions, and the flow between these actions. From initialization through error handling, the process has been defined to ensure that administrators have a clear roadmap for this component’s operation, suitable for use in environments requiring high-contrast interfaces.

