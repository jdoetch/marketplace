# Censys ASM - Add tags for a web entity

## Overview
The "Censys ASM - Add tags for a web entity" component automates the process of tagging web entities with relevant tags based on specific criteria. This automation plays a crucial role in managing web assets effectively by categorizing them based on their characteristics or criteria which helps in improving the ease of management and enhancing security posture.

## Summary of the Component
This component, enabled within the Censys asset management framework, engages in automated tagging operations to systematically label web entities using defined tags. The process ensures that each tagged entity meets certain conditions reflective of their business or security classifications.

### Process Flow Summary
1. **Initiation**: The process begins upon the identification of a web entity that requires tagging.
2. **Tag Generation**: Based on predefined criteria or fetched data, suitable tags are generated for the web entity.
3. **Tag Application**: The generated tags are then applied to the identified web entity.
4. **Verification**: Post-application, a verification step confirms the accuracy and relevance of the tag applied.
5. **Completion**: Upon successful verification, the process concludes, and if any discrepancies are found, remedial actions are undertaken.

### Detailed Actions
- **Step 1: Initiation**:
  - **Type**: Trigger
  - **Purpose**: Detects the presence or creation of a new web entity that requires tagging.
  - **On-success**: Proceed to Tag Generation.
  - **On-failure**: Log the error and terminate the process.

- **Step 2: Tag Generation**:
  - **Type**: Data Processing
  - **Purpose**: Determines suitable tags for the web entity based on specific attributes or external data sources.
  - **On-success**: Move to Tag Application.
  - **On-failure**: Retry the tag generation or escalate.

- **Step 3: Tag Application**:
  - **Type**: Update Operation
  - **Purpose**: Applies the generated tags to the specified web entity within the Censys ASM.
  - **On-success**: Verify the tagging process.
  - **On-failure**: Attempt to re-apply the tags or escalate.

- **Step 4: Verification**:
  - **Type**: Audit Check
  - **Purpose**: Ensures that all tags are correctly applied and are reflective of the current attributes of the web entity.
  - **On-success**: Conclude the tagging process.
  - **On-failure**: Remove incorrect tags and repeat the process from Tag Generation.

- **Step 5: Completion**:
  - **Type**: Notification/Logging
  - **Purpose**: Records the successful completion of the tagging process or logs any issues for further investigation.

This workflow ensures that all web entities within the Censys ASM are consistently and accurately tagged, facilitating improved management and security monitoring.
