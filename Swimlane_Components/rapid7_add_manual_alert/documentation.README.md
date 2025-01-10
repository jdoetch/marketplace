# Rapid7 Threat Command - Add Manual Alert Technical Documentation

## Overview
This document serves as the detailed technical documentation for the "Rapid7 Threat Command - Add Manual Alert" component. Aimed for security professionals and system administrators, this document breaks down the functionalities and flow of actions within the component to aid in deployment and troubleshooting.

### Reason for Existence
The "Rapid7 Threat Command - Add Manual Alert" component exists to enable users to manually input alerts into the Threat Command system, enhancing the organization's ability to respond swiftly to identified threats.

### Process Flow Summary
The process begins with the initiation of the "Add Manual Alert" action which contains several fields such as description, severity, source attributes, and more filled by the user. On successful completion of this action, results are transformed and presented accordingly. Failures in the action lead to no subsequent operations.

### Detailed Action Breakdown

#### Add Manual Alert
- **Type**: Connector
- **Description**: Initializes the manual addition of an alert based on user-generated input.
- **Inputs**:
  - **description**: User-provided description of the alert.
  - **severity**: Severity level of the alert.
  - **date**: Date of the alert event.
  - **source**:
    - **source type**: Type of source reporting the alert.
    - **network type**: Network classification involved in the alert.
    - **url**: URL involved in the alert scenario.
  - **image files**: Associated image evidence.
- **Verify SSL**: Ensures secure connection.
- **On Success**:
  - Process transitions to the result transformation stage.
- **On Failure**:
  - No further actions are processed.

#### Component Result
- **Type**: Transformation
- **Description**: Manages and formats the results of the alert addition operation.
- **Details**:
  - **Expressions**: Evaluate the existence of a response text; processes the error message if present.
  - **Outcome**:
    - **On Success**: Display and handle the formatted response.
    - **On Failure**: Stop operations, log failure details.

### Complete Workflow
1. User triggers the Add Manual Alert action.
2. System processes the inputs and attempts to add the alert.
3. Upon success:
   - The result is prepared and processed for final presentation.
4. Upon failure:
   - Error is logged, and no further action is taken.

This document should assist in the comprehensive understanding and effective management of the "Rapid7 Threat Command - Add Manual Alert" component within security operations.
