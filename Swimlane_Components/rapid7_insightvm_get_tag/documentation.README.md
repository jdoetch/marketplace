# Rapid7 InsightVM - Get Tag Component Documentation

## Overview
This document details the **Rapid7 InsightVM - Get Tag** component, designed for efficiently retrieving asset tag information within the InsightVM environment. This component leverages the Rapid7 InsightVM API to extract detailed information about an asset's tag, aiding in asset management and security operations.

## Component Summary
The **Rapid7 InsightVM - Get Tag** component encompasses various actions which facilitate the querying and retrieval of asset tag details from the InsightVM platform. This component is vital for security teams and asset managers who require detailed insight into asset identification within their network environments.

## Actions Detail
### Get Tag
- **Type**: Connector
- **Description**: Retrieves the tag information for a specified asset.
- **Inputs**:
  - **Path Parameters**: The ID of the asset for which tag information is required.
  - **Verify SSL**: Boolean to verify SSL certificate.
- **On-Success**: Proceed to display the result.
- **On-Failure**: The action does not have a specified failure path; it stops execution.
- **On-Complete**: Triggers the component result transformation action.

### Component Result
- **Type**: Transformation
- **Description**: Processes the results from the Get Tag action and prepares it for user consumption.
- **Transformations**:
  - **Result Display**:
    - **Condition**: Checks if the Get Tag action has succeeded and results are available.
    - **Action**: Displays the result if available; otherwise, notifies that the retrieval failed.
- **On-Success**: N/A
- **On-Failure**: N/A
- **On-Complete**: N/A

## Process Flow Summary
1. **Initiation**: Triggered manually or by another process, the Component begins by executing the Get Tag action.
2. **Get Tag Execution**: The Get Tag action calls the InsightVM API with specific asset ID parameters to fetch tag information.
3. **Result Processing**: Upon successful retrieval, the Component Result action processes the output from the Get Tag action, handling the data and preparing it for display or further analysis.
4. **Completion**: The process either displays the detailed tag information fetched or indicates a failure if the data cannot be retreived.

## Usage
The **Rapid7 InsightVM - Get Tag** component is utilized within the default pool, ensuring resource optimization and effective load handling. It is primarily aimed at enhancing asset management practices by providing critical tag details essential for security posture assessment and compliance.

## Versioning and Updates
- **Version**: This document applies to version 1.0 of the Rapid7 InsightVM - Get Tag component.
- **Modified By**: Modified by Jay Spann, as per the documentation provided.
- **Modification Date**: Updated usage and error handling pathways to streamline operations and decrease potential downtime.

## Conclusion
The component serves as a crucial tool in asset management by simplifying the retrieval of asset tag details, essential for maintaining an up-to-date and secure IT infrastructure. This document should serve as a foundation for implementing and understanding the component within various IT environments.
