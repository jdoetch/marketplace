# SSC - Search Companies in Bulk Documentation

## Overview
The "SSC - Search Companies in Bulk" component is designed to enable streamlined, bulk searching capabilities within a system, which is crucial for efficient data management and operational efficiency in business environments. The component allows automated workflows that are robust and highly customizable, enhancing productivity and data consistency.

## Summary of the Component
This component involves multiple automated actions that initiate with data querying and extend to in-depth data enrichment processes. It operates on a transformation model wherein initial error data is enriched to provide a comprehensive output that is detailed and immediately usable. The process is built on a condition/response mechanism, making it capable of handling multiple input variations and errors.

### Process Flow
1. **Start with Error Capture**:
   - **Action Type**: Transformation.
   - **Purpose**: To transform the error data into a structured format.
   - **On-Success**: Proceed to data enrichment.
   - **On-Failure**: Log error and halt the process.

2. **Data Enrichment**:
   - **Sub-Action**: Error Enrichment.
   - **Purpose**: To enrich the error data with additional metadata like timestamp, permalink, and raw data based on the type and source of the error.
   - **Type**: JSON transformation.
   - **On-Complete**: Post the enriched data.

3. **Post Actions**:
   - **Purpose**: To publish and/or store the enriched data for downstream use.
   - **Publishing Mechanism**: Referral to the results of the Data Enrichment action.

## Detailed Action Descriptions

### Error Capture Action
- **Description**: This initial action deals with capturing and structuring the input error data.
- **Inputs Required**:
  - Error Provider
  - Error Status
  - Error Result
- **Outputs**:
  - Structured error information ready for enrichment.
- **Success Criteria**: Data is correctly structured without any loss or misinterpretation.
- **Failure Management**: Errors are logged with a timestamp and details, and the process is terminated.

### Error Enrichment Action
- **Description**: This action enriches the input error data by adding detailed contextual information.
- **Input Data**:
  - **Enrichment Provider**: Taken dynamically from the error data.
  - **Enrichment Type**: Specified as "reputation".
  - **Enrichment Verdict**: Specified in the process definition.
- **Output**:
  - Enriched data that includes timestamps, direct links (permalinks), and raw data.
- **Dependencies**:
  - Successful completion of the Error Capture action.
- **Completion Handling**: On completion, the enriched data is formatted for publishing according to predefined schemas.

## Overall Process Flow Summary
The component operates in a sequence of error handling, data transformation, and enrichment, culminating in the distribution of thoroughly processed data. Each action is delineated by clear success or failure paths, ensuring robust handling of processes and data integrity. The use of JSON data transformation techniques ensures high versatility and integration capability with various data sources and downstream systems.

