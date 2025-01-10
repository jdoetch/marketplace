# Component Documentation: `Recorded Future Sandbox Enrichment Component`

## Overview

The component facilitates the enrichment of observables by integrating with Recorded Future's sandbox environment. It processes observables such as URLs and files to provide contextual enrichment, verdicts, and detailed reports. This component orchestrates various actions including observable metadata mapping, conditional parallel processing, enrichment verdict generation, and error handling.

---

## Actions Overview

### 1. **Create Enrichment Variables**
   - **Type**: `createVariables`
   - **Purpose**: Initializes variables required for enrichment processing.
   - **Inputs**:
     - `Enrichment_Provider`: Recorded Future Sandbox
     - `observable_value`: Observable value provided by the input.
   - **Next Steps**:
     - **On-Success**: `Map_Observable_Metadata_to_Value`

---

### 2. **Map Observable Metadata to Value**
   - **Type**: `connector`
   - **Purpose**: Maps observable metadata to corresponding values.
   - **Inputs**:
     - `observable_value`: Observable value.
     - `observable_metadata`: Metadata related to the observable.
   - **Next Steps**:
     - **On-Success**: `Update_Observable_Value`

---

### 3. **Update Observable Value**
   - **Type**: `updateVariables`
   - **Purpose**: Updates the observable value based on the mapping results.
   - **Next Steps**:
     - **On-Success**: `Conditional_Parallel`

---

### 4. **Conditional Parallel**
   - **Type**: `parallelGroup`
   - **Purpose**: Processes observables based on their type (URL or file).
   - **Entrypoints**:
     - **URL Submission**: If the observable is a URL.
     - **File Submission**: If the observable is a file.
   - **Actions**:
     - `Url Lookup`: Submits the URL for analysis and generates enrichment.
     - `File submisison (via URL fetch)`: Submits the file for sandbox analysis.

---

#### URL Handling

##### **URL Submission**
   - **Type**: `conditional`
   - **Purpose**: Determines if the observable is a URL and submits it to the sandbox.
   - **Next Steps**:
     - **On-Success**: `Submit URL to SB`

##### **Submit URL to SB**
   - **Type**: `connector`
   - **Purpose**: Submits a URL to the Recorded Future Sandbox for analysis.
   - **Inputs**:
     - `url`: URL observable value.
   - **Next Steps**:
     - **On-Success**: `Get URL summary report from SB`

##### **Get URL Summary Report from SB**
   - **Type**: `connector`
   - **Purpose**: Retrieves the analysis report for the submitted URL.
   - **Next Steps**:
     - **On-Success**: `Create TEDS Enrichment URL SB Submission`

##### **Create TEDS Enrichment URL SB Submission**
   - **Type**: `transformation`
   - **Purpose**: Generates enrichment data from the URL analysis report.
   - **Steps**:
     - Generates verdicts (`malicious`, `suspicious`, `benign`, or `unknown`) based on risk scores.
     - Provides enrichment metadata, including permalink and context.
   - **Next Steps**:
     - **On-Success**: `Update Enrichment (URL submission)`

##### **Update Enrichment (URL submission)**
   - **Type**: `updateVariables`
   - **Purpose**: Updates the enrichment variables with the generated URL enrichment data.

---

#### File Handling

##### **File Submission (via URL Fetch)**
   - **Type**: `conditional`
   - **Purpose**: Determines if the observable is a file and submits it for analysis.
   - **Next Steps**:
     - **On-Success**: `Post file sample via URL-fetch`

##### **Post File Sample via URL-Fetch**
   - **Type**: `connector`
   - **Purpose**: Submits the file to the Recorded Future Sandbox for analysis.
   - **Inputs**:
     - `url`: URL pointing to the file.
   - **Next Steps**:
     - **On-Success**: `Get File Summary Report`

##### **Get File Summary Report**
   - **Type**: `connector`
   - **Purpose**: Retrieves the analysis report for the submitted file.
   - **Next Steps**:
     - **On-Success**: `Create TEDS Enrichment File SB Submission`

##### **Create TEDS Enrichment File SB Submission**
   - **Type**: `transformation`
   - **Purpose**: Generates enrichment data from the file analysis report.
   - **Steps**:
     - Generates verdicts (`malicious`, `suspicious`, `benign`, or `unknown`) based on risk scores.
     - Provides enrichment metadata, including permalink and context.
   - **Next Steps**:
     - **On-Success**: `Update Enrichment (File submission)`

##### **Update Enrichment (File submission)**
   - **Type**: `updateVariables`
   - **Purpose**: Updates the enrichment variables with the generated file enrichment data.

---

### 5. **Error Handling**

#### URL Errors
- **Actions**:
  - `CreateTEDSErrorEnrichment_URL_Lookup`
  - `CreateTEDSErrorEnrichment_File_submission`
- **Purpose**: Captures and processes errors during URL or file enrichment.

#### File Errors
- **Actions**:
  - `CreateTEDSErrorEnrichment_File_submission`
- **Purpose**: Captures and processes errors during file analysis.

---

## Process Flow Summary

1. **Initialization**: The process begins with `Create Enrichment Variables` to prepare the input variables.
2. **Mapping**: `Map Observable Metadata to Value` maps the input observable data.
3. **Processing**:
   - **For URLs**: Submits the URL to the sandbox, retrieves the report, and generates enrichment.
   - **For Files**: Submits the file to the sandbox, retrieves the report, and generates enrichment.
4. **Error Handling**: Captures errors in submission or analysis processes and logs the results.
5. **Update Enrichment**: Finalizes the enrichment data and updates variables for further processing or reporting.

This structured component ensures efficient enrichment and analysis of observables while providing robust error handling and detailed contextual data for threat intelligence purposes.