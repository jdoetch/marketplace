# Group-IB Component Technical Documentation

## Overview

This component automates the retrieval and processing of alerts from the Group-IB system. It defines parameters for filtering alerts, fetches the alert data, and processes them to generate enriched alert entries. The component ensures actionable insights by transforming raw alert data and integrating it into a structured format.

---

## Actions Overview

### 1. Create Variables for VIC
- **Type**: `createVariables`
- **Purpose**: Initializes variables for storing provider and alert details.
- **Subsequent Steps**:
  - On Success: Proceeds to the **Create Parameters** action.
  - On Failure/Complete: None.
- **Inputs**:
  - `Provider`: Default value set to `"Group-IB"`.
  - `Alerts`: An empty list `[]`.

---

### 2. Create Parameters
- **Type**: `transformation`
- **Purpose**: Defines filtering and sorting parameters for retrieving alerts from Group-IB.
- **Subsequent Steps**:
  - On Success: Executes the **Get Alerts** action.
  - On Failure/Complete: None.
- **Details**:
  - **Transformations**:
    - Creates a JSON object with keys: `createdAt__gte`, `Sort By`, `Limit`, and `Query`.

---

### 3. Get Alerts
- **Type**: `http`
- **Purpose**: Fetches alerts based on the defined parameters.
- **Subsequent Steps**:
  - On Success: Proceeds to **Get Results** action.
  - On Failure: None.
  - On Complete: None.
- **Inputs**:
  - **Endpoint**: `https://huntbox.de.group-ib.com/api/v1/alerts/check/`
  - **Method**: `POST`
  - **Body**: Includes the `search` parameter with filtering logic, such as a date range.

---

### 4. Get Results
- **Type**: `transformation`
- **Purpose**: Processes the response from **Get Alerts** to determine the number of results and extract alert data.
- **Subsequent Steps**:
  - On Success: Proceeds to **If Resources Available to Process - Check** action.
  - On Failure/Complete: None.
- **Details**:
  - **Transformations**:
    - Extracts the total count of alerts and their details.

---

### 5. If Resources Available to Process - Check
- **Type**: `conditional`
- **Purpose**: Verifies if there are alerts to process.
- **Subsequent Steps**:
  - On Success: Proceeds to **Loop Over Alerts** action.
  - On Else: Terminates the workflow.

---

### 6. Loop Over Alerts
- **Type**: `loop`
- **Purpose**: Iterates through each alert to process its data.
- **Subsequent Steps**:
  - On Success: Executes the **Get Alerts** action.
  - On Failure/Complete: None.
- **Actions**:
  - **Alert Field Definitions**: Transforms raw alert data into enriched fields like category, severity, timestamps, and titles.
  - **Parse Observables**: Enriches observables associated with alerts.

---

### 7. Update Alerts
- **Type**: `updateVariables`
- **Purpose**: Updates the global `Alerts` variable with processed alert data.
- **Subsequent Steps**:
  - None.
- **Inputs**:
  - `Alerts`: Populated with the enriched alert data.

---

## Process Flow Summary

1. **Initialize Variables**: The workflow begins by creating variables for the provider and alerts.
2. **Define Parameters**: Filters and sorting criteria for alert retrieval are established.
3. **Retrieve Alerts**: The system fetches alerts using the Group-IB API.
4. **Check for Alerts**: If alerts are available, the workflow processes them. Otherwise, it terminates.
5. **Process Alerts**: Iterates through alerts to extract and transform key data fields.
6. **Enrich Observables**: Identifies and processes observables like hashes, IPs, and emails.
7. **Update Alerts**: Stores the enriched alerts into the global `Alerts` variable.

---

## Inputs and Outputs

### Inputs
- **Filter**: Date filter for retrieving alerts.
- **Offset**: Pagination control.
- **Sort**: Defines sorting criteria.
- **Limit**: Restricts the number of alerts retrieved.
- **Query**: Additional filtering logic.

### Outputs
The component outputs enriched alerts, including metadata such as:
- Alert UID, Category, Title, Severity.
- MITRE ATT&CK tactics and techniques.
- Associated observables and timestamps.

---

This documentation is designed for end-users who require a structured overview of the Group-IB alert processing component.