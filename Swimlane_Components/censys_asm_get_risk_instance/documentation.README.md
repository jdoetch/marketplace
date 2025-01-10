# Censys ASM - Get Risk Instance Technical Documentation

## Overview
The "Censys ASM - Get Risk Instance" component is designed to enhance security automation by providing detailed risk assessments from Censys ASM. This component automates the process of fetching risk instances, helping organizations quickly identify and mitigate potential threats at scale.

## Summary of the Component
This component interacts with the Censys ASM API to pull detailed information about specific risk instances. By automating this process, it aims to streamline the workflow involved in risk detection and remediation.

### Actions
The component includes a key action:
- **Enrichment - Create Error**: A transformation type action meant to enrich error data collected during the risk detection process.
  - **Type**: Transformation
  - **Description**: This action enriches the error data which includes provider details and the nature of the error.
  - **On Success**: Proceeds to the next step based on the defined workflow.
  - **On Failure**: Triggers defined failure handling mechanisms.
  - **On Complete**: Completes the action and optionally triggers post-action events.

#### Subsequent Steps:
- **Publish**: Output is directed towards the specified endpoint, typically within the same organizational infrastructure for integration with other processes.
- **Transformations**: Specific transformation called `teds_error_enrichment` is applied to structure the enriched error data effectively.

### Overall Process Flow Summary
1. **Data Fetching**: Initially, data concerning specific risk instances is gathered from the Censys ASM.
2. **Enrichment**: The gathered data undergoes enrichment where additional details relevant for analysis are appended.
3. **Publishing**: Once the enrichment is completed, the data is published or sent forward as defined within the component, making it available for further analysis or integration.

This flow ensures that risk instance data collected is detailed, timely, and formatted for immediate use in security operations.

