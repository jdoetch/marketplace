# API Void - Get Domain Age Component Documentation

## Overview
The API Void - Get Domain Age Component allows users to determine the registration date and age of a domain, providing valuable information for security assessments and digital investigations. This component is integrated through HTTP requests to the APIVoid service's endpoint.

## Component Summary
This component executes a HTTP request to fetch the domain age data. The process involves passing domain details and processing the response to extract crucial details about the domain's registration timeline.

### Actions
The component contains a main action named `Domain Age`:

- **Type**: HTTP
- **Purpose**: To facilitate the retrieval of domain registration dates and the age in days from APIVoid.
- **On-Success**: Not specified
- **On-Failure**: Not specified
- **On-Complete**: Not specified
- **Inputs**:
  - **Endpoint**: https://endpoint.apivoid.com/domainage/v/pay-as-you-go/
  - **Method**: HTTP GET
  - **Headers**: None
  - **Query Parameters**:
    - **Key**: host
    - **Value**: {dynamic value based on input}
    - **Description**: Enter the domain to check the domain age.
- **Settings**:
  - **Follow Redirects**: true
  - **Verify Certificates**: true
  - **Allow Unsafe Legacy Renegotiation**: false

### Process Flow
1. **Initialization**: The component starts with the input of a domain name by the user.
2. **HTTP Request**: A request is made to the specified endpoint with the domain as a query parameter.
3. **Response Processing**: On receiving the response, the domain age data is extracted.
4. **Completion**: The component handles the completion of the action with no specific post-execution action defined.

## Environment and Settings
- **Assets Required**: oid_key
- **Execution Pool**: Default
- **Output Schema Referenced**: bfbc-fd---ebabcd (specifies the formatting of the output data)

This component leverages precise settings to ensure secure and accurate HTTP requests to the APIVoid service.

### Testing and Validation
- The component has been set up with test inputs mimicking the real request format.
- Validation confirms that the overall setup is correct and functional.

## Conclusion
The API Void - Get Domain Age component is essential for users requiring information on the age of a domain, which can be critical for various cybersecurity and digital forensic processes.

