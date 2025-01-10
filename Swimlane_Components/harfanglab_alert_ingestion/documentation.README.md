# Component: HarfangLab Get Alert Component

## Overview
The **cHarfangLab Get Alert Component** automates the detection, processing, and enrichment of alerts using a series of transformations, condition checks, and external integrations. This component is designed to efficiently process detection data, extract relevant metadata, and aggregate observables for further analysis.

The component follows a structured process that starts with variable creation, evaluates resource availability, iterates over alerts for enrichment, and subsequently processes and publishes enriched alert data.

---

## Actions Overview

### 1. **Create Variables for VIC**
**Type**: `createVariables`  
**Purpose**: Initializes variables for the component.  
**Inputs**:
- `Provider`: Hardcoded as `HarfangLab`
- `Alerts`: An empty list

**Next Steps**:  
On-success → **Create Parameters**

---

### 2. **Create Parameters**
**Type**: `transformation`  
**Purpose**: Generates the required parameters for alert retrieval.  
**Inputs**:
- Parameters like `filter`, `offset`, `sort`, `limit`, and `q`.

**Next Steps**:  
On-success → **GetAlerts**

---

### 3. **GetAlerts**
**Type**: `connector`  
**Purpose**: Fetches alerts from HarfangLab using a connector.  
**Inputs**:  
- Parameters: Passed from the previous transformation  
- `verify_ssl`: `true`  
**Action**: `harfanglab.fetch_incidents`  

**Next Steps**:  
On-success → **If Resources Available to Process - Check**

---

### 4. **If Resources Available to Process - Check**
**Type**: `conditional`  
**Purpose**: Checks if resources are available to process further detections.  
**Conditions**:
- Verifies if the alert count from `GetAlerts` is greater than `0`.  

**Next Steps**:  
On-success → **Loop Over Detections**

---

### 5. **Loop Over Detections**
**Type**: `loop`  
**Purpose**: Iterates over detection data for enrichment.  
**Entrypoint**: **Alert Field Definitions**  

#### Sub-Actions within the Loop:
1. **Alert Field Definitions**
   **Type**: `transformation`  
   **Purpose**: Processes individual alerts to extract metadata and enrich observables.  
   - **alert_uid**: Extracts the alert unique identifier.  
   - **alert_category**: Combines alert type and subtype.  
   - **alert_start_timestamp**: Captures the start timestamp of the alert.  
   - **alert_end_timestamp**: Extracts the timestamp field `@timestamp`.  
   - **alert_created_timestamp**: Captures the event creation timestamp.  
   - **alert_provider**: Retrieves the provider name (`variables.Provider`).  
   - **alert_severity**: Extracts alert severity level.  
   - **alert_title**: Constructs a descriptive title with the alert message and impacted host.  
   - **alert_rules**: Extracts alert rules from `rule_content` using a JSONata expression.  
   - **alert_mitre_attack_tactic_technique**: Maps MITRE ATT&CK tactics and techniques using `mitre_cells`.  
   - **alert_ingested_timestamp**: Adds the current ingestion timestamp.  
   - **concatenate_observable_fields**: Combines hash values (MD5, SHA1, SHA256) for observables.  
   - **alert_risk_score**: Captures the risk score of the alert.  
   - **alert_impacted_hostnames**: Lists impacted hostnames.  
   - **alert_impacted_usernames**: Lists impacted usernames.  
   - **raw_alert**: Publishes the raw alert data.

   **Next Steps**:  
   On-success → **Parse Observables**

2. **Parse Observables**
   **Type**: `connector`  
   **Purpose**: Processes concatenated observable fields for enrichment.  
   **Inputs**: Text value extracted from concatenated observables.

   **Next Steps**:  
   On-success → **Create TEDS Alert**

3. **Create TEDS Alert**
   **Type**: `connector`  
   **Purpose**: Generates a final alert with all enriched data and observables.  
   **Inputs**:
   - Alert metadata (UID, timestamps, rules, impacted hosts/users, MITRE ATT&CK details).

---

### 6. **Get Alerts**
**Type**: `transformation`  
**Purpose**: Aggregates alert data from the previous enrichment cycle.  
**Inputs**:  
Uses a lookup function to retrieve enriched alerts.  

**Next Steps**:  
On-success → **Update Alerts**

---

### 7. **Update Alerts**
**Type**: `updateVariables`  
**Purpose**: Updates the `Alerts` variable with the enriched and processed alert data.  
**Inputs**:
- `Alerts`: Updated with results from **Get Alerts**.

---

## Process Flow Summary

1. **Initialization**: Variables are created for the provider and alert list.  
2. **Alert Retrieval**: Alerts are fetched using an external connector.  
3. **Resource Check**: The component verifies if alerts are available for processing.  
4. **Enrichment Loop**: For each alert:
   - Extracts and processes metadata, including timestamps, risk scores, impacted hosts, usernames, and observables.
   - Maps MITRE ATT&CK tactics and techniques.  
5. **Observables Processing**: Enriches observables using connectors.  
6. **Final Alert Creation**: Constructs a comprehensive alert object with enriched details.  
7. **Aggregation**: Combines all processed alerts.  
8. **Update**: Updates the main `Alerts` variable with the aggregated results.

---

## Key Features
- **Scalability**: Loops over multiple alerts and processes each alert individually.
- **Enrichment**: Extracts key metadata (timestamps, risk scores, MITRE details) for deeper insights.
- **Observables Aggregation**: Combines and processes file hashes and related fields.
- **Integration**: Utilizes external connectors for alert fetching and processing.

---

## Inputs
- `filter`: Optional filter for alerts.  
- `offset`: Specifies an offset for pagination.  
- `sort`: Sorting preference for alerts.  
- `limit`: Number of alerts to retrieve.  
- `q`: Query parameters for advanced filtering.

---

## Outputs
The component outputs an enriched list of alerts containing:
- Unique identifiers (UID)
- Timestamps (start, end, ingestion, creation)
- Alert metadata (category, provider, severity, risk score)
- Impacted hosts and usernames
- MITRE ATT&CK tactics and techniques
- Observables (file hashes and other enriched fields)
- Raw alert data for further analysis.

---

## Conclusion
The **component_aYnvXLwhQJ752fcb5** efficiently processes detection data, enriching it with detailed metadata and observables. It integrates seamlessly with external services, ensuring comprehensive alert creation and aggregation for end-user analysis.