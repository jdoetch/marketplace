# Component: `Recorded Future Sandbox Enrichment VIC`

## Overview

The `Recorded Future Sandbox Enrichment VIC` is designed to handle the submission and analysis of observables (URLs, files, etc.) through Recorded Future’s sandbox and enrichment API. It evaluates observables, processes reputation data, and generates structured enrichment information for use in further incident response workflows.

---

## Actions Overview

### **Create Enrichment Variables**
- **Type**: Create Variables  
- **Purpose**: Initializes key variables required for the enrichment process, including `Enrichment_Provider`, `observable_value`, and an empty `Enrichment` array.  
- **On-Success**: Proceeds to `Map Observable Metadata to Value`.

---

### **Map Observable Metadata to Value**
- **Type**: Connector  
- **Purpose**: Extracts and maps metadata from the observable to create a meaningful `observable_value`.  
- **On-Success**: Updates the `observable_value` variable via `Update Observable Value`.

---

### **Update Observable Value**
- **Type**: Update Variables  
- **Purpose**: Updates the `observable_value` variable based on the extracted metadata.  
- **On-Success**: Initiates `Conditional Parallel`.

---

### **Conditional Parallel**
- **Type**: Parallel Group  
- **Purpose**: Manages multiple conditional paths for processing supported observable types.  
- **Entrypoints**:
  - **`URL_submission`**: Handles URL submissions.
  - **`Filesubmission_to_Sandbox`**: Handles file submissions.

#### **URL Submission**
- **Type**: Conditional  
- **Purpose**: Checks if the observable type is a URL and triggers `Submit URL to SB` if true.

#### **File Submission (via URL Fetch)**
- **Type**: Conditional  
- **Purpose**: Checks if the observable type is a file and triggers `Post file sample via URL-fetch` if true.

---

### **Submit URL to SB**
- **Type**: Connector  
- **Purpose**: Submits the URL to Recorded Future’s sandbox for analysis.  
- **On-Success**: Retrieves the analysis report using `Get URL Summary Report from SB`.

---

### **Get URL Summary Report from SB**
- **Type**: Connector  
- **Purpose**: Fetches the summary report for the submitted URL from the sandbox.  
- **On-Success**: Proceeds to `Create TEDS Enrichment URL SB Submission`.

---

### **Create TEDS Enrichment URL SB Submission**
- **Type**: Transformation  
- **Purpose**: Processes the sandbox report to generate enrichment data, including verdict, timestamp, permalink, and context.  
- **On-Success**: Updates the enrichment variable with the generated data.

---

### **Post File Sample via URL-Fetch**
- **Type**: Connector  
- **Purpose**: Submits a file sample (via URL) to Recorded Future’s sandbox for analysis.  
- **On-Success**: Retrieves the file analysis report using `Get File Summary Report`.

---

### **Get File Summary Report**
- **Type**: Connector  
- **Purpose**: Fetches the summary report for the submitted file from the sandbox.  
- **On-Success**: Proceeds to `Create TEDS Enrichment File SB Submission`.

---

### **Create TEDS Enrichment File SB Submission**
- **Type**: Transformation  
- **Purpose**: Processes the file analysis report to generate enrichment data for the file.  
- **On-Success**: Updates the enrichment variable with the generated file data.

---

### **Error Handling**
#### **Create TEDS Error Enrichment**
- **Type**: Connector  
- **Purpose**: Handles errors during URL or file submission and generates an error enrichment record.  

---

## Process Flow Summary

1. Initialize enrichment variables.  
2. Map observable metadata and update the observable value.  
3. Evaluate the observable type and process it using the appropriate conditional path.  
4. Submit the observable (URL or file) to Recorded Future’s sandbox for analysis.  
5. Retrieve the sandbox analysis report and generate enrichment data.  
6. Handle errors gracefully by generating error enrichment records.  

---

## Inputs

- **observable**:  
  - **observable_value**: The value of the observable to be enriched. *(Required)*  
  - **observable_type**: The type of the observable (e.g., URL, file). *(Required)*  
  - **observable_metadata**: Additional metadata associated with the observable.

---

## Outputs

- **Enrichment**:  
  - Includes enrichment provider, verdict, timestamp, permalink, context, and raw data.

---

## Key Features

- Supports the submission and analysis of URLs and files through Recorded Future’s sandbox.  
- Provides structured enrichment data for use in security operations workflows.  
- Handles errors gracefully and ensures comprehensive logging of failures.  
- Integrates seamlessly with Recorded Future’s API for reputation analysis.