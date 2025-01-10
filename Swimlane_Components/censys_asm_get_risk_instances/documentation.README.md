# Censys ASM - Get Risk Instances Component

## Short Description
The "Censys ASM - Get Risk Instances" component is crafted to assist users in querying and retrieving risk instance data from the Censys ASM platform. The primary reason this flow exists is to automate the process of risk assessment and mitigation. It ensures that users can dynamically fetch risk statuses related to assets and help maintain an updated security posture.

## Summary of the Component
This component acts as an intermediary to extract potential risk data by interacting with the Censys API. The flow executes a series of actions, mainly HTTP requests for retrieving risk instances and processing the data to align with the user's security frameworks.

## Actions Overview
### 1. `create_variables`
- **Type**: Creation
- **Purpose**: Initializes variables required for further processes.
- **Subsequent Steps**:
  - **On Success**: Proceeds to the `_request` action.

### 2. `_request`
- **Type**: HTTP Request
- **Purpose**: Sends a request to the Censys API endpoint to retrieve risk instance data.
- **Subsequent Steps**:
  - **On Success**: Triggers the `create_enrichment` action.
  - **On Failure**: Initiates `normalize_createerror_atwc`.

### 3. `create_enrichment`
- **Type**: Transformation
- **Purpose**: Transforms the data received from the `_request` action into a suitable format.
- **Subsequent Steps**:
  - **On Success**: Proceeds to `update_enrichment`.

### 4. `normalize_createerror_atwc`
- **Type**: Connector
- **Purpose**: Handles errors from the `_request` action.
- **Subsequent Steps**:
  - **On Success**: Redirects to `update_enrich`.

### 5. `update_enrichment`
- **Type**: Update Variables
- **Purpose**: Updates the enrichment details with newly transformed data.
- **Subsequent Steps**:
  - **On Success**: Completes the flow unless there are additional directives.

## Overall Process Flow Summary
The component starts by creating necessary variables for the operation. It then executes an API request to Censys to fetch risk data. Depending on the success or failure of this API call, it either processes the risk data for usability or handles errors. The processed data is then updated, culminating the flow if all actions succeed.

### Technical Requirements
This component requires API access to Censys with appropriate permissions to fetch risk instance data. Ensure all parameters like endpoint details and query parameters are accurately set in the configuration.

### Security Aspects
It adheres to secure practices by verifying certificates and following redirects judiciously during HTTPS requests.

## Usage
To utilize this component:
1. Ensure API keys and endpoints are configured correctly.
2. Review and adjust the query parameters according to the data requirement.
3. Execute the component in an environment that complies with your security standards.
