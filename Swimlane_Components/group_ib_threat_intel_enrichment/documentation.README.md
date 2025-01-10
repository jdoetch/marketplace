# Component: `Group-IB Threat Intel Component`

## Overview

The `Group-IB Threat Intel Component` is designed to enrich observables by integrating with Group-IB’s intelligence API. It evaluates the reputation of observables, provides context, and generates enrichment data for further use. This component handles different observable types such as IPs, domains, URLs, hashes, and files, enabling detailed threat intelligence workflows.

---

## Actions Overview

### 1. **Create Enrichment Variables**
   - **Type**: Create Variables  
   - **Purpose**: Initializes variables needed for enrichment, such as `Enrichment_Provider`, `observable_value`, and an empty `Enrichment` array.  
   - **On-Success**: Proceeds to `Map_Observable_Metadata_to_Value`.

---

### 2. **Map Observable Metadata to Value**
   - **Type**: Connector  
   - **Purpose**: Maps metadata from the observable to generate a meaningful observable value.  
   - **On-Success**: Triggers `updateVariables_agdvf` to set the observable value.

---

### 3. **Update Observable Value**
   - **Type**: Update Variables  
   - **Purpose**: Updates the `observable_value` variable based on the results from the previous step.  
   - **On-Success**: Initiates the `Conditional_Parallel` action.

---

### 4. **Conditional Parallel**
   - **Type**: Parallel Group  
   - **Purpose**: Executes various conditional actions in parallel for supported observable types.  
   - **Entrypoints**: Includes `IPURLDomainHash` and subsequent enrichment actions.
   - **On-Complete**: Triggers a no-operation (`NOOP`) action.

---

#### **IP/URL/Domain/Hash/File**
   - **Type**: Conditional  
   - **Purpose**: Evaluates the observable type to determine if it is supported (e.g., IP, domain, hash, file).  
   - **On-Success**: Calls `Get_Observable_Reputation`.

#### **Get Observable Reputation**
   - **Type**: Connector  
   - **Purpose**: Queries Group-IB’s API for observable reputation data.  
   - **On-Success**: Triggers `Create_TEDS_Enrichment`.  
   - **On-Failure**: Triggers `Create_TEDS_Error_Enrichment`.

---

### 5. **Create TEDS Enrichment**
   - **Type**: Transformation  
   - **Purpose**: Processes the observable reputation data to generate enrichment details such as verdict, timestamp, permalink, and context.  
   - **On-Success**: Proceeds to `Update_Enrichment_Reputation`.

---

#### **Enrichment Sub-Actions**
   - **Enrichment Verdict**: Determines if the observable is `Benign`, `Suspicious`, or `Malicious` based on reputation results.  
   - **Enrichment Timestamp**: Records the current timestamp for the enrichment.  
   - **Enrichment Permalink**: Creates a permalink for viewing enrichment data in Group-IB’s dashboard.  
   - **Enrichment Context**: Provides contextual information about the observable based on its reputation.  
   - **Enrichment**: Aggregates all enrichment data into a structured format.

---

### 6. **Update Enrichment (Reputation)**
   - **Type**: Update Variables  
   - **Purpose**: Updates the `Enrichment` variable with the processed reputation data.  
   - **On-Success**: Completes the workflow.

---

### 7. **Create TEDS Error Enrichment**
   - **Type**: Connector  
   - **Purpose**: Generates an error enrichment in case reputation retrieval fails.  
   - **On-Success**: Triggers `Update_Enrichment_Error_Reputation`.

---

### 8. **Update Enrichment (Error: Reputation)**
   - **Type**: Update Variables  
   - **Purpose**: Updates the `Enrichment` variable with error details for failed reputation actions.

---

### 9. **NOOP**
   - **Type**: Transformation  
   - **Purpose**: Placeholder action to mark the end of the parallel group.

---

## Process Flow Summary

1. Initializes enrichment variables.
2. Maps observable metadata to generate a meaningful value.
3. Executes conditional actions to evaluate observable types.
4. Retrieves reputation data or handles errors.
5. Processes and enriches the reputation data with details such as verdict, timestamp, permalink, and context.
6. Updates the enrichment data or logs errors if the enrichment fails.

---

## Inputs

- **observable**:  
  - **observable_type**: Type of the observable (e.g., IP, domain, hash, file). *(Required)*  
  - **observable_value**: Value of the observable to be enriched. *(Required)*  
  - **observable_metadata**: Additional metadata for the observable.

---

## Outputs

- **Enrichment**:  
  - Type: Enriched data or error details.  
  - Includes provider, verdict, timestamp, permalink, context, and raw reputation data.

---

## Key Features

- Supports multiple observable types (IP, URL, domain, hash, file).  
- Integrates with Group-IB’s intelligence API for detailed reputation insights.  
- Provides structured enrichment data for use in downstream workflows.  
- Handles errors gracefully with dedicated error enrichment workflows.