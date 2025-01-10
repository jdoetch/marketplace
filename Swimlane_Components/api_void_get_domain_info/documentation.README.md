# API Void - Get Domain Info - Technical Documentation

## Overview
The API Void - Get Domain Info component allows users to retrieve comprehensive domain-related information with ease. This component harnesses the capabilities of the API Void service to extract details such as the domain registrar, ownership, and nameservers among others. Primarily aimed at automating investigations and checks related to domain information, this component becomes a strategic tool in security operations and domain management.

## Summary of the Component
The component interacts with an API provided by API Void to fetch domain details. It focuses on streamlining the process to extract domain information in real-time, using pre-configured settings and inputs for optimized performance and accuracy.

## Actions Detail
- **Domain Info Action**: 
  - **Type**: HTTP
  - **Description**: Fetches domain WHOIS details like registrar, ownership, and nameservers.
  - **Endpoints**: `https://endpoint.apivoid.com/domaininfo/v/pay-as-you-go/`
  - **Method**: GET or POST (based on final implementation)
  - **Query Parameters**:
    - **Host**: Specifies the domain to retrieve information. Example: `swimlane.com`
  - **Settings**:
    - **Follow Redirects**: Enabled
    - **Verify Certificates**: Enabled
    - **Allow Unsafe Legacy Negotiation**: Disabled
  - **Success Criteria**: Action returns domain information successfully.
  - **Failure Handling**: Reroutes to error logging or alternative flows based on the configuration.

### Process Flow Summary
1. **Initiation**: Triggered manually or via external events.
2. **Data Retrieval**:
   - API call to API Void with specified parameters.
   - Check for proper execution and capture error codes or failures.
3. **Parsing & Output**:
   - On successful API call, parse the JSON/XML response.
   - Extract and publish relevant information per requirements.
4. **Completion**:
   - Publish the results for downstream processing or alerting.
   - Log and handle any errors or anomalies encountered.

This process ensures a thorough and efficient method of obtaining domain-related data aiding in various investigative and monitoring tasks.

### Connectivity and Assets
The component utilizes the `oid_key` asset for authenticated interaction with the API Void service. Secure handling and management of this asset are paramount for operation.

### Endpoints Design
Endpoints are designed to be fault-tolerant with settings like verified SSL certificates and redirection following, which ensures reliable data fetch operations under varying network conditions.

### Data Integrity and Security
Utilizes built-in configurations to maintain the integrity and confidentiality of the data being handled, integrating seamlessly into existing security frameworks and compliance standards.

### Versioning and Updates
- **Initial Release**: Based on the created date, authored by Swimlane.
- **Maintenance & Updates**: Regular updates are provided in response to API changes, feature enhancements, and security improvements.

## Error Management and Logging
Detailed logging of both successful and failed events allows for comprehensive monitoring and troubleshooting. Failure paths include error capture and notifications to appropriate channels to take necessary actions swiftly.

## Conclusion
The API Void - Get Domain Info component offers a sophisticated capability for automating the retrieval and analysis of domain-related information, ensuring that users can maintain high levels of operational efficiency and security awareness.

### Additional Information
For detailed API specifications and further configuration options, please refer to the API Void documentation and support.

