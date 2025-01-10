# Rapid7 InsightVM - Get Asset Vulnerabilities

## Overview

Rapid7 InsightVM's component "Get Asset Vulnerabilities" serves to automate the retrieval of vulnerability information for specified assets. This documentation outlines the technical specification, flow, and actions associated with this component.

### Summary

The "Get Asset Vulnerabilities" component is designed to automate processes within IT security infrastructure, particularly focusing on the detailed assessment and timely update of asset vulnerabilities. This component interacts with Rapid7 InsightVM's APIs to fetch vulnerabilities based on given asset identifiers.

### Detailed Process Flow

- **Start**: The component begins with a trigger or manual input specifying the necessary asset details.
- **Action**: "Get Asset Vulnerabilities"
  - **Type**: Connector
  - **Purpose**: To add an asset and pass the required and optional inputs to fetch pages(s) of vulnerabilities related to that asset.
  - **Input Parameters**:
    - **Asset ID**: Unique identifier for the asset whose vulnerabilities are required.
    - **Page**: Specifies the pagination page.
    - **Size**: Specifies the number of records per page.
    - **Verify SSL**: A boolean to specify SSL verification status.
  - **Subsequent Steps**:
    - **On-Success**: Proceeds to the result transformation phase.
    - **On-Failure**: There is no follow-up action defined for failure; hence it terminates.
    - **On-Complete**: Calls the "Component Result" to transform and publish the findings.

### Component Result

- **Title**: Component Result
- **Type**: Transformation
- **Purpose**: Used to structure and possibly convert the vulnerability data fetched from the InsightVM into a meaningful format.
- **Subsequent Steps**:
  - **Data Transformation and Publication**: Transform the results into required formats and possibly trigger other workflows or alerts based on the results.

### Overall Process

1. **Trigger/Input**: Receive asset details.
2. **Query Rapid7 InsightVM**: Fetch vulnerability details using the specified inputs.
3. **Data Processing**: Transform the vulnerability details.
4. **Completion**: Output is either published for further action or the workflow ends.

This component integrates seamlessly into existing security environments, enhancing the automation capabilities of vulnerability management. It ensures that security teams have up-to-date information on potential vulnerabilities affecting their digital assets.

