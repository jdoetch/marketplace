# SecurityTrails - Fetch WHOIS History By Domain Documentation

## Overview
The "SecurityTrails - Fetch WHOIS History By Domain" component is designed to provide a detailed historical lookup of WHOIS data associated with domain names. This capability is essential for security research and analysis, allowing users to trace the ownership and historical changes of domain registrations, which is a fundamental aspect in investigation and threat intelligence.

## Summary of the Component
This component integrates with the SecurityTrails API to fetch WHOIS history by domain name. It systematically queries for domain-related information, handles the response, and processes the data to present the user with comprehensive details regarding domain registration changes over time.

## Prerequisites

In order to authenticate against the Security Trails API, you need an api key.

## API Setup

To get an API key please see the API Docs, https://docs.securitytrails.com/docs/authentication

## Process and Workflow

### Action: Enrichment - Create Error
#### Type: Transformation
- **Purpose:** This action is used to handle and transform errors returned by the SecurityTrails API into a more structured error format for easier debugging and logging.
- **On-Success:** Proceeds to the next step in the process flow depending on the workflow configuration.
- **On-Failure:** Logs the error details and terminates the process or retries as configured.
- **Details:**
  - Input includes error details such as provider, status code, and error message.
  - Transformation logic formats these inputs into a structured error document.

### General Process Flow Summary
1. **Initiation**: Triggered manually or by a predefined condition in the system.
2. **Fetch WHOIS History**: A request is made to the SecurityTrails API to retrieve the WHOIS history by domain.
3. **Error Handling**: If the API returns an error, the 'Enrichment - Create Error' action is taken. The error received is structured for better clarity and logged.
4. **Data Processing**: On successful data retrieval, the information is processed and formatted as required for further use either within the system or for analytical purposes.
5. **Completion**: The process either ends on successful execution or after handling an error.

## Additional Notes
- This component is enabled and fully supports automated operations, ensuring that WHOIS data lookup is consistent and efficient.
- The configuration of actions includes error handling to maintain robustness of the component under different operational conditions.

This documentation is intended to offer a comprehensive guide to using and understanding the "SecurityTrails - Fetch WHOIS History By Domain" component in security research and operational contexts.

