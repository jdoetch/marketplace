# Rapid7 InsightVM - Get Scan Details Component Documentation

## Overview
The **Rapid7 InsightVM - Get Scan Details** component is designed to enhance automation in security operations by allowing users to retrieve comprehensive details of a given scan quickly. This capability can be instrumental in understanding the security landscape and making informed decisions based on scan outcomes.

## Component Summary
This component interfaces with Rapid7 InsightVM to fetch detailed information about a specific scan. Through a structured process involving multiple actions, it ensures that users receive precise scan information, which is crucial for effective vulnerability management and security automation.

### Actions Detailed Description

#### Get Scan
- **Type:** Connector
- **Description:** Initiates a connection with Rapid7 InsightVM to fetch scan details. It takes an asset identifier as input and communicates with the InsightVM API to retrieve the data.
- **Inputs:**
  - **id (Asset Identifier):** The unique identifier of the scan for which details are required.
  - **verify_ssl:** A boolean parameter that enables SSL verification.
- **Pool:** $default
- **On-Success:** Proceeds to the transformation step.
- **On-Failure:** Typically, it would handle exceptions or errors that occur while fetching the scan details.

#### Component Result (Transformation)
- **Type:** Transformation
- **Description:** Processes the data retrieved from the Get Scan action. This action prepares the data for downstream consumption or integration.
- **On-Complete:** Designates the result processing and storage.
- **Transformations:**
  - **Result:**
    - **Description:** Transforms the retrieved JSON data into a format suitable for further use or display.
    - **Display:** Configured for advanced display settings.
    - **Inputs:**
      - **Data Path:** Extracts and transforms the JSON data based on existing conditions.

## Process Flow Summary
1. **Get Scan**: This primary action is triggered to fetch the scan details from Rapid7 InsightVM utilizing the scan ID provided.
2. **Transformation**: Upon successful data retrieval, the component processes the data ensuring it is in the proper format for use.
3. **Result Handling**: The transformed data is then either displayed or further used as input for other systems or reports.

The **Rapid7 InsightVM - Get Scan Details** component ensures that detailed and actionable scan information is readily available to improve the security posture efficiently and effectively.

