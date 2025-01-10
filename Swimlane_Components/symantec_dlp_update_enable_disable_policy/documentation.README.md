# Symantec DLP - Update (Enable/Disable) Policy Technical Documentation

## Overview

This document provides the technical documentation for the "Symantec DLP - Update (Enable/Disable) Policy" component. The component provides the functionality to update Symantec Data Loss Prevention (DLP) policies by either enabling or disabling them. This component is particularly useful in scenarios where automated, conditional management of data security policies is required.

## Summary of the Component

The Symantec DLP - Update (Enable/Disable) Policy component aims to streamline the management process of Symantec's DLP policies through automation. This involves updating the state of a policy based either on predefined criteria or operational requirements, enhancing the adaptability and responsiveness of data loss prevention mechanisms.

## Action Descriptions

### Update a Policy Action

- **Type**: Connector
- **Description**: This action allows for the enablement or disablement of a designated Symantec DLP policy. Enabling the policy is performed by setting the 'enable' parameter to true.
- **Inputs**:
  - `policy_id`: Identifier of the policy to be updated.
  - `enable`: Boolean value determining whether the policy should be enabled (true) or disabled (false).
  - `verify_ssl`: Boolean value for SSL verification.
- **Process Flow**:
  - **Success**: Proceed to component result.
  - **Failure**: No specific failure action designated; errors should be handled as per system default settings or external error handling policies.
  - **Completion**: Publishes the result.

### Component Result Action

- **Type**: Transformation
- **Description**: This action transforms and provides the result based on the outcome of the policy update operation.
- **Process Flow**:
  - **Data Handling**: Checks if the policy update action's result is present and can determine the success or failure of the operation.
  - **Output**: Displays the result.

## Overall Process Flow Summary

1. **Starting Point**: The component is triggered with required inputs such as 'policy_id' and 'enable'.
2. **Action Execution**: The update policy action is initiated, and the system tries to enable or disable the specified policy based on the input values.
3. **Result Handling**: Depending on the success or failure of the action, the result is transformed and presented.
4. **Completion**: The component either ends successfully after updating the policy and displaying the result, or logs a failure which needs to be addressed.

## Conclusion

This component is essential for organizations utilizing Symantec DLP by providing a means to agilely manage data loss prevention policies through automation, thus facilitating better compliance and data security standards.

