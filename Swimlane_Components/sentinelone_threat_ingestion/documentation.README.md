# Overview

This playbook automates the process of retrieving and enriching threat data from SentinelOne. It evaluates available threat information, loops through detected threats, and processes them to generate enriched threat entries. The playbook leverages conditional checks, transformations, and SentinelOne API integrations to ensure high-quality threat insights.

---

# Actions Overview

## 1. Create Variables for VIC
- **Type**: `createVariables`
- **Purpose**: Initializes global variables to store provider and threat data.
- **On Success**:
  - Proceeds to the `Create Parameters` action.
- **Details**:
  - **Inputs**:
    - `Provider`: Default value is `"SentinelOne"`.
    - `Alerts`: An empty list `[]`.

---

## 2. Create Parameters
- **Type**: `transformation`
- **Purpose**: Sets up filtering and sorting parameters for threat retrieval.
- **On Success**:
  - Proceeds to the `Get Threats` action.
- **Details**:
  - **Transformations**:
    - Builds a JSON object with keys like `createdAt__gte`, `Sort By`, `Limit`, and `Query`.

---

## 3. Get Threats
- **Type**: `connector`
- **Purpose**: Fetches threat data from SentinelOne using the defined parameters.
- **On Success**:
  - Proceeds to the `If Resources Available to Process - Check` action.
- **Details**:
  - **Inputs**:
    - `parameters`: Derived from the `Create Parameters` action.
    - `verify_ssl`: Enabled (`true`).
  - **Connector**: `sentinelone.get_threats`.

---

## 4. If Resources Available to Process - Check
- **Type**: `conditional`
- **Purpose**: Verifies whether there are any threats available for processing.
- **On Success**:
  - Proceeds to the `Loop Over Enrichment` action.
- **Else**:
  - Ends the workflow.
- **Conditions**:
  - Checks if `pagination.totalItems` > 0 in the retrieved threats.

---

## 5. Loop Over Enrichment
- **Type**: `loop`
- **Purpose**: Iterates through each threat for detailed processing and enrichment.
- **On Success**:
  - Executes the `Alert Field Definitions` action.
- **Details**:
  - **Entrypoints**:
    - `Alert_Field_Definitions`.

---

## 6. Alert Field Definitions
- **Type**: `transformation`
- **Purpose**: Extracts and transforms key details from each threat.
- **On Success**:
  - Proceeds to the `Parse Observables` action.
- **Details**:
  - **Transformations**:
    - `alert_uid`: Extracts the unique identifier of the threat.
    - `alert_category`: Categorizes the threat based on its classification.
    - `alert_title`: Generates a descriptive title summarizing the threat's impact.
    - `alert_severity`: Determines the severity of the threat based on predefined criteria.

---

## 7. Parse Observables
- **Type**: `connector`
- **Purpose**: Parses observables associated with the threat for further analysis.
- **On Success**:
  - Proceeds to the `Create TEDS Alert` action.
- **Details**:
  - **Inputs**:
    - `text_value`: Derived from concatenated observable fields.

---

## 8. Create TEDS Alert
- **Type**: `connector`
- **Purpose**: Creates enriched threat entries with all metadata and observables.
- **Details**:
  - **Inputs**:
    - Metadata fields such as `alert_uid`, `alert_category`, `alert_severity`, and `alert_provider`.

---

## 9. Get Threat
- **Type**: `transformation`
- **Purpose**: Fetches enriched threat data for further processing.
- **On Success**:
  - Proceeds to `Update Threats`.
- **Details**:
  - **Transformations**:
    - Enriches threat data by combining metadata and observable fields.

---

## 10. Update Threats
- **Type**: `updateVariables`
- **Purpose**: Updates the global `Alerts` variable with processed threat data.
- **Details**:
  - **Inputs**:
    - `Alerts`: Populated with the enriched threat data.

---

# Process Flow Summary

1. **Initialize Variables**:
   - Creates variables to store provider and threat data.
2. **Define Parameters**:
   - Sets up filtering and sorting criteria for threat retrieval.
3. **Retrieve Threats**:
   - Fetches threats from SentinelOne based on the defined parameters.
4. **Check for Threats**:
   - Verifies if threats are available; if none, the workflow ends.
5. **Process Threats**:
   - Loops through each threat and extracts key information such as severity, timestamps, and observables.
6. **Create Enriched Threats**:
   - Generates enriched threat entries and logs metadata.
7. **Update Variables**:
   - Updates the `Alerts` variable with the latest enriched data.

---

# Output

The playbook updates the `Alerts` variable with enriched threat data, including metadata, severity, and observables, ensuring it reflects the most recent threat information.
