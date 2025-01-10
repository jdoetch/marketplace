# Censys ASM - Add Tag to a Host

## Introduction
The "Censys ASM - Add Tag to a Host" component is designed to automate the process of tagging hosts within the Censys ASM platform, which is essential for organizing and managing assets based on specific criteria like security posture, department, or any custom tag that suits the user's operations.

## Component Overview
This component simplifies the workflow of adding tags to hosts by interfacing with the Censys ASM API. It handles various tasks such as creating necessary variables, handling API requests, and managing data transformations to ensure that tags are added correctly and efficiently. 

## Actions Description
### Create Variables
- **Type**: `create_variables`
- **Purpose**: Initializes variables used in the tagging process.
- **On-Success**:
  - Proceed to make an HTTP request to add the tag.
- **On-Failure**: 
  - No subsequent action defined; the process is halted.

### HTTP Request
- **Type**: `http`
- **Purpose**: Performs the API call to Censys ASM to add a tag to a specified host.
- **Inputs**:
  - `endpoint`: URL constructed to access the specific host's tag addition endpoint.
  - `headers`, `method`, `body`: Configured to align with API requirements.
- **On-Success**:
  - Triggers the "Create Enrichment" action if the API request is successful.
- **On-Failure**:
  - Triggers the "Normalize Create Error At WC" action to handle potential errors.
- **Complete**: 
  - No subsequent action defined; the process is concluded for the HTTP action.

### Create Enrichment
- **Type**: `transformation`
- **Purpose**: Handles the transformation of data received from the host to format it for enrichment purposes.
- **On-Success**:
  - Updates enrichment with the newly created data.
- **On-Failure**: 
  - The process is halted with no further action.

### Update Enrichment
- **Type**: `update_variables`
- **Purpose**: Sets the created enrichment data into the appropriate variables for further use.
- **On-Failure**:
  - No specific failure action is defined; ends the process.

### Normalize Create Error at WC
- **Type**: `connector`
- **Purpose**: Normalizes and logs the errors received from the Censys ASM API call.
- **On-Success**:
  - Updates the enrichment process possibly with error details for logging.
- **On-Failure**: 
  - No specific action defined; usually ends the error handling.

## Overall Process Flow Summary
This component follows a systematic approach to add tags to hosts in Censys ASM:
1. Initialize variables needed for the process.
2. Conduct an API request to Censys ASM for tagging a host.
3. On successful API call, process the response for any necessary enrichment.
4. Transform and update enrichment variables with relevant data from the response.
5. Handle any errors from the API request, normalize and log them appropriately.

Given its structured flow, this component ensures efficient and error-free tagging of hosts, thereby enhancing the management and categorization of assets within the Censys ASM platform.
