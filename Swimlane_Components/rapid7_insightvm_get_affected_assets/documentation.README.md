# Rapid7 InsightVM - Get Affected Assets - Technical Documentation

## Overview
This document serves as comprehensive technical guidance for the "Rapid7 InsightVM - Get Affected Assets" component. This component facilitates the identification of enterprise assets impacted by specific vulnerabilities, integrating seamlessly with the Rapid7 InsightVM environment to enhance security measures and vulnerability management.

## Component Summary
The "Rapid7 InsightVM - Get Affected Assets" component plays a critical role in automating the retrieval of asset information based on given vulnerabilities. The component interacts with the Rapid7 InsightVM via defined connectors, performing actions to retrieve and transform data regarding affected assets.

### Actions Detailed

#### Get Affected Assets Action
- **Type:** Connector
- **Purpose:** Retrieves a list of assets affected by specified vulnerabilities, enhancing the response to potential security threats.
- **On-Success:** Proceeds to result transformation.
- **On-Failure:** There is a defined failure handling routine, ensuring alternative measures are considered.
- **Inputs:** Requires vulnerability ID (`id`) provided via path parameters.
- **Outputs:** Directs output towards transformation component.

#### Component Result Transformation
- **Type:** Transformation
- **Purpose:** Transforms and formats the data retrieved from the "Get Affected Assets" action for further usage or reporting.
- **On-Success:** Successfully completes the data handling process.
- **On-Failure:** Handles any data transformation errors.
- **Outputs:** Generates a final output in a predetermined format detailing the affected assets.

## Process Flow
1. **Start:** Triggering of the component via internal or external calls.
2. **Action Execution:** The "Get Affected Assets" action is executed, attempting to fetch data from Rapid7 InsightVM based on input parameters.
3. **Data Handling:** Upon successful data retrieval, the information is directed to the Transformation stage.
4. **Transformation:** Data is reformatted and prepared for final output.
5. **Completion:** Process completes with data either successfully transformed or an error handled accordingly.

## Failure Management
Ensures robust error handling at each stage, providing fallbacks and error information to enable quick troubleshooting and corrective actions.

## Security and Compliance
Adheres to strict security protocols with SSL verification and controlled access to ensure data integrity and confidentiality in interactions with the Rapid7 InsightVM.

## Versioning Information
- **Component Version:** Drafted in the current system state.
- **Last Modified:** Automatically updates with modification in the system.

## Conclusion
The "Rapid7 InsightVM - Get Affected Assets" component is essential for effective vulnerability management, providing critical capabilities for rapid identification and response to security threats.

