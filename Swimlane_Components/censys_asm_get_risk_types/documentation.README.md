# Censys ASM - Get Risk Types - Technical Documentation

## Overview
The Censys ASM - Get Risk Types component is designed to integrate with security automation workflows to identify and categorize various risk types associated with assets in a network. This component leverages the capabilities of the Censys ASM platform to enhance security posture by providing insights into potential vulnerabilities.

## Component Summary
The purpose of this component is to automate the process of fetching risk type data from Censys ASM and integrate this data into broader security management practices. By automating this task, organizations can more efficiently identify risks and prioritize their mitigation efforts accordingly.

### Actions
#### Enrichment - Create Error
- **Type:** Transformation
- **Purpose:** This action handles errors that might occur during data fetch operations from the Censys ASM. It enriches the error data for better clarity and management.
- **Subsequent Steps:**
  - **On-Success:** Proceed to the next step in the workflow.
  - **On-Failure:** Trigger error handling mechanisms.
  - **On-Complete:** Conclude this action element of the component.

##### Transformations
- **Error Enrichment**
  - **Description:** Structures and enhances error information to provide detailed insights.
  - **Inputs:** Includes error provider, status, and results.
  - **Action Type:** JSONata

### Process Flow
1. **Start**: Initiate the component.
2. **Fetch Risk Types**: Attempt to gather risk type data from Censys ASM.
3. **Error Handling**: In case of failures, enrich and structure error data.
4. **Data Integration**: On successful fetch, integrate risk type data into the security ecosystem.
5. **Completion**: End the process.

### Overall Flow Summary
The component starts by fetching risk data. Upon successful fetch, it seamlessly integrates this data into existing security systems, enhancing the overall security posture. In the event of an error during the fetch process, the error is caught, enriched, and managed properly, allowing for smooth continuation or termination of the workflow based on the nature of the error.

### Conclusion
The Censys ASM - Get Risk Types component is essential for organizations looking to automate aspects of their security operations. By efficiently categorizing and handling risk-related data, this component aids in fortifying security measures against potential threats.
