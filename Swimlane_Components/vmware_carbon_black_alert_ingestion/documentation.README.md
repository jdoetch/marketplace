# Overview

This playbook automates the process of enriching and handling alerts using Carbon Black. It evaluates incoming alert data, loops through detections for enrichment, and creates enriched alert entries with metadata and timestamps. The playbook ensures accurate and actionable insights through conditional checks, transformations, and VMWARE Carbon Black API interactions.

---

# Actions Overview

## 1. Get Oldest Timestamp
- **Type**: `component`
- **Purpose**: Takes a human-readable string and returns ISO8601 and Unix timestamps.
- **On Success**:
  - Proceeds to the `Build Filter` action.
- **Details**:
  - **Inputs**:
    - `Human Readable String`: Accepted format is '(+|-) x seconds|minutes|hours|days|years ago|from now|in the future|in the past' or 'now'.  For example, 'now'  '10 seconds ago', '3 years from now', '-10 minutes', '+1 hour'.
  - **Outputs**:
    - `Result`: an object containing the following keys: ISO8601, epocj, milliseconds

---
## 2. Build Filter
- **Type**: `transformation`
- **Purpose**: Takes the ISO8601 timestamp and formats a filter and query.
- **On Success**:
  - Proceeds to the `CArbon Black Get Alerts` action.
- **Details**:
  - **Transformations**:
     - Builds a JSON object with keys like `Filter` and `Query`.
---

## 3. Create Variables for VIC
- **Type**: `createVariables`
- **Purpose**: Initializes variables to store provider and alert details.
- **On Success**:
  - Proceeds to the `Create Parameters` action.
- **Details**:
  - **Inputs**:
    - `Provider`: Default value is `"Carbon Black"`.
    - `Alerts`: An empty list `[]`.

---

## 4. Create Parameters
- **Type**: `transformation`
- **Purpose**: Defines the filtering and sorting parameters for retrieving alerts.
- **On Success**:
  - Proceeds to the `Get Alerts` action.
- **Details**:
  - **Transformations**:
    - Builds a JSON object with keys like `Parameters`, `CB Start Time`, and `CB End Time`.

---

## 5. Get Alerts
- **Type**: `connector`
- **Purpose**: Fetches alert data from Carbon Black using the configured parameters.
- **On Success**:
  - Proceeds to `Loop Over Enrichment`.
- **Details**:
  - **Inputs**:
    - `Org Key`: Derived from the `CB_EDR_SIEM_API_Key` asset.
    - `start`: Derived from the `Create Parameters` action.
    - `end`: Derived from the `Create Parameters` action.
    - `URL`: Derived from the `CB_EDR_SIEM_API_Key` asset.
    - `API ID`: Derived from the `CB_EDR_SIEM_API_Key` asset.
    - `API Secret`: Derived from the `CB_EDR_SIEM_API_Key` asset.
  - **Connector**: `vmware_carbon_black_cloud.get_alerts`.

---


## 6. Loop Over Enrichment
- **Type**: `loop`
- **Purpose**: Iterates through each alert to perform detailed enrichment and processing.
- **On Success**:
  - Executes the `Alert Field Definitions` action.
- **Details**:
  - **Entrypoints**:
    - `Alert_Field_Definitions`.

---

## 7. Alert Field Definitions
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

## 8. Parse Observables
- **Type**: `connector`
- **Purpose**: Parses and enriches observables from the alert.
- **On Success**:
  - Proceeds to `Create TEDS Alert`.
- **Details**:
  - **Inputs**:
    - `text_value`: Derived from concatenated observable fields.

---

## 9. Create TEDS Alert
- **Type**: `connector`
- **Purpose**: Creates an enriched alert entry in the system, including all metadata and observables.
- **Details**:
  - **Inputs**:
    - Metadata fields such as `alert_uid`, `alert_category`, `alert_severity`, and `alert_provider`.

---

## 10. Get Alerts
- **Type**: `transformation`
- **Purpose**: Extracts an array of TEDS Alerts with enriched alert data from the loop.
- **Details**:
  - **Inputs**:
    - `Alerts`: Populated with the enriched alert data.

---

# Process Flow Summary


 
1. **Get Oldest Timpstamp**:
   - The playbook begins by getting a timestamp.
2. **Build Filter**:
   - Sets up the ingestion filter.
3. **Initialize Variables**:
   - Creating global variables to store provider and alert details.
4. **Define Parameters**:
   - Sets up the filtering and sorting criteria for alert retrieval.
5. **Retrieve Alerts**:
   - Fetches alerts from Carbon Black using the defined parameters.
6. **Enrich Alerts**:
   - Loops through each alert, extracting key information like timestamps, categories, and observables.
7. **Create Enriched Alerts**:
   - Generates enriched alert entries and logs metadata.
8. **Finalize Alerts**:
   - Collects an array of the processed alert data.

---

# Output

The playbook updates the `Alerts` variable with enriched data, including metadata and observables, ensuring it reflects the latest state of processed alerts.
