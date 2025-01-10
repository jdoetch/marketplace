# Technical Documentation: Criminal IP - Get Suspicious Info

## Overview
The "Criminal IP - Get Suspicious Info" component is designed to enhance cybersecurity measures by collecting and analyzing data related to suspicious IP addresses. This component seamlessly integrates into security workflows, allowing automated gathering and processing of IP-related intelligence, which is crucial for early detection of potential threats.

## Summary of the Component
This component involves several actions geared towards the transformation and enrichment of error data related to suspicious IPs by invoking external services or APIs that provide reputation scores and other relevant details. Successful execution of these actions can significantly aid in the process of security analysis and threat mitigation.

### Actions
The component includes the following key actions:
1. **Create Error Enrichment**  
   - **Type**: Transformation
   - **Purpose**: To transform error data into actionable intelligence by enriching it with additional context such as reputation information.
   - **On-Success**: Proceed to the next step if the action succeeds.
   - **On-Failure**: Retry or halt the process based on the configuration.
   - **On-Complete**: Finalize the enrichment process and publish the results.

### Process Flow
1. **Initialization**: The process begins by capturing error information related to suspicious IPs.
2. **Transformation**: The error data undergoes a transformation where it is enriched with external data, such as reputation scores.
3. **Publish Results**: Once the data is enriched, the results are published for further use in the cybersecurity infrastructure.
4. **Completion**: The process is marked complete, and all outcomes (success or failure) are logged for audit purposes.

## Detailed Action Descriptions
### Create Error Enrichment
This action involves the enrichment of IP-related error data by incorporating external intelligence:
   - **Inputs**:
     - `error_provider`: The source of the error data.
     - `error_status`: The status of the error.
     - `error_result`: The result or output of the error analysis.
   - **Transformation**: Data is enriched based on the input parameters using a configured external provider that supplies IP reputation information.
   - **Outputs**:
     - Enriched data which includes enhanced attributes like IP reputation, timestamp of enrichment, and links to detailed reports.

## Conclusion
In summary, the "Criminal IP - Get Suspicious Info" component is pivotal in enhancing security operations. By automating the process of data enrichment for suspicious IPs, it empowers security teams to quickly identify and mitigate potential threats, ensuring a robust defense against cyber-attacks.
