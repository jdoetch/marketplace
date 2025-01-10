# Symantec DLP - Get Incident Correlations

## Overview
The **Symantec DLP - Get Incident Correlations** component is designed to automate the process of retrieving incident correlation data within the Symantec Data Loss Prevention framework. This component is crucial for organizations looking to streamline their incident analysis and response strategies by leveraging Symantec's robust security platform.

## Component Summary
This component integrates with the Symantec DLP system to fetch detailed correlation data related to specific security incidents. By automating this process, the component aids in reducing response times and enhancing the accuracy of security incident investigations.

### Actions
#### Get Incident Correlations
- **Type**: Connector
- **Purpose**: Fetches correlation details related to an incident from Symantec DLP.
- **Inputs**:
  - **path_parameters**:
    - **id**: Incident ID (required to fetch relevant data).
  - **verify_ssl**: Boolean to decide SSL verification enabling.
- **Post-action steps**:
  - **On-success**: Proceed to **Component Result** processing.
  - **On-failure**: Typically, triggers error handling workflows or logs the failure for further analysis.

#### Component Result
- **Type**: Transformation
- **Purpose**: Handles the output from the Get Incident Correlations action, transforming it into a usable format for further processes or storage.
- **Details**:
  - Designed to manage data transformation with potential for broad application in reporting and alerting pipelines.
- **Outputs**:
  - Transforms incident correlation data to suit needs of downstream systems or processes.

### Overall Process Flow
1. **Initialization**: The component is triggered by a need to fetch correlation data for a specified incident.
2. **Execution**: The **Get Incident Correlations** action is executed, which interacts with the Symantec DLP to retrieve the necessary data.
3. **Data Handling**:
   - **On Success**: Data fetched successfully passes to the **Component Result** action.
   - **On Failure**: Error paths are evaluated, potentially triggering alerts or logs.
4. **Post-Execution**: Transformed data is either sent to other systems for further action or aggregated in a central data store for reporting and analysis.

By implementing this automated process, organizations can ensure the timely and accurate gathering of incident-related data, thereby improving overall security posture and incident response capabilities.

