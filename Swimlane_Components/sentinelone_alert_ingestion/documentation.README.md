# Overview

This playbook automates the process of enriching and handling alerts using SentinelOne. It evaluates incoming alert data, loops through detections for enrichment, and creates enriched alert entries with metadata and timestamps. The playbook ensures accurate and actionable insights through conditional checks, transformations, and SentinelOne API interactions.

---

# Actions Overview

## 1. Create Variables for VIC
- **Type**: `createVariables`
- **Purpose**: Initializes variables to store provider and alert details.
- **On Success**:
  - Proceeds to the `Create Parameters` action.
- **Details**:
  - **Inputs**:
    - `Provider`: Default value is `"SentinelOne"`.
    - `Alerts`: An empty list `[]`.

---

## 2. Create Parameters
- **Type**: `transformation`
- **Purpose**: Defines the filtering and sorting parameters for retrieving alerts.
- **On Success**:
  - Proceeds to the `Get Alerts` action.
- **Details**:
  - **Transformations**:
    - Builds a JSON object with keys like `createdAt__gte`, `Sort By`, `Limit`, and `Query`.

---

## 3. Get Alerts
- **Type**: `connector`
- **Purpose**: Fetches alert data from SentinelOne using the configured parameters.
- **On Success**:
  - Proceeds to `If Resources Available to Process - Check`.
- **Details**:
  - **Inputs**:
    - `parameters`: Derived from the `Create Parameters` action.
    - `verify_ssl`: Enabled (`true`).
  - **Connector**: `sentinelone.get_alerts`.

---

## 4. If Resources Available to Process - Check
- **Type**: `conditional`
- **Purpose**: Verifies whether there are alerts available for processing.
- **On Success**:
  - Proceeds to `Loop Over Enrichment`.
- **Else**:
  - Ends the workflow.
- **Conditions**:
  - Checks if `pagination.totalItems` > 0 in the retrieved alerts.

---

## 5. Loop Over Enrichment
- **Type**: `loop`
- **Purpose**: Iterates through each alert to perform detailed enrichment and processing.
- **On Success**:
  - Executes the `Alert Field Definitions` action.
- **Details**:
  - **Entrypoints**:
    - `Alert_Field_Definitions`.

---

## 6. Alert Field Definitions
- **Type**: `transformation`
- **Purpose**: Extracts and transforms critical alert information such as category, timestamps, and severity.
- **On Success**:
  - Proceeds to `Parse Observables`.
- **Details**:
  - **Transformations**:
    - `alert_uid`: Extracts the unique identifier of the alert.
    - `alert_category`: Identifies the category of the alert based on its indicators.
    - `alert_title`: Generates a descriptive title for the alert.

---

## 7. Parse Observables
- **Type**: `connector`
- **Purpose**: Parses and enriches observables from the alert.
- **On Success**:
  - Proceeds to `Create TEDS Alert`.
- **Details**:
  - **Inputs**:
    - `text_value`: Derived from concatenated observable fields.

---

## 8. Create TEDS Alert
- **Type**: `connector`
- **Purpose**: Creates an enriched alert entry in the system, including all metadata and observables.
- **Details**:
  - **Inputs**:
    - Metadata fields such as `alert_uid`, `alert_category`, `alert_severity`, and `alert_provider`.

---

## 9. Update Alerts
- **Type**: `updateVariables`
- **Purpose**: Updates the global variable `Alerts` with enriched alert data.
- **Details**:
  - **Inputs**:
    - `Alerts`: Populated with the enriched alert data.

---

# Process Flow Summary

1. **Initialize Variables**:
   - The playbook begins by creating global variables to store provider and alert details.
2. **Define Parameters**:
   - Sets up the filtering and sorting criteria for alert retrieval.
3. **Retrieve Alerts**:
   - Fetches alerts from SentinelOne using the defined parameters.
4. **Check for Alerts**:
   - If alerts are available, processes them further. Otherwise, ends the workflow.
5. **Enrich Alerts**:
   - Loops through each alert, extracting key information like timestamps, categories, and observables.
6. **Create Enriched Alerts**:
   - Generates enriched alert entries and logs metadata.
7. **Update Alerts**:
   - Updates the global `Alerts` variable with the processed alert data.

---

# Output

The playbook updates the `Alerts` variable with enriched data, including metadata and observables, ensuring it reflects the latest state of processed alerts.
