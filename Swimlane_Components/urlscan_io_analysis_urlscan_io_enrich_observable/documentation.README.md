# Overview

This playbook automates the enrichment of observables using URLScan. It defines variables, evaluates observable types, retrieves reputation data, and generates enriched metadata. The playbook ensures accurate and actionable insights by combining conditional checks, data transformations, and API interactions with URLScan.

---

# Actions Overview

## 1. Create Enrichment Variables
- **Type**: `createVariables`
- **Purpose**: Initializes variables to define the enrichment provider and response array.
- **On Success**:
  - Proceeds to `Map Observable Metadata to Value`.
- **Details**:
  - **Inputs**:
    - `Enrichment_Provider`: Default value is `"URLScan"`.
    - `Enrichment`: An empty list `[]`.
    - `observable_value`: Extracted from the input observable's value.

---

## 2. Map Observable Metadata to Value
- **Type**: `connector`
- **Purpose**: Maps observable metadata to its respective value for further processing.
- **On Success**:
  - Proceeds to `Conditional Parallel`.
- **Details**:
  - **Inputs**:
    - `observable`: Derived from the input observable object.

---

## 3. Conditional Parallel
- **Type**: `parallelGroup`
- **Purpose**: Handles multiple conditions for processing observables.
- **Entrypoints**:
  - **IP/URL/Domain/Hash/File**:
    - **Type**: `conditional`
    - **Purpose**: Evaluates whether the observable is a supported type.
    - **On Success**:
      - Proceeds to `Submit Observable`.
    - **Conditions**:
      - Observable types such as `ipv4_public`, `ipv6_public`, `domain`, and `url` are supported.

---

## 4. Submit Observable
- **Type**: `connector`
- **Purpose**: Submits the observable to URLScan for reputation analysis.
- **On Success**:
  - Proceeds to `Get Observable Reputation`.
- **Details**:
  - **Inputs**:
    - `json_body`: Includes the observable value.
    - `verify_ssl`: Enabled (`true`).

---

## 5. Get Observable Reputation
- **Type**: `connector`
- **Purpose**: Retrieves reputation information from URLScan for the submitted observable.
- **On Success**:
  - Proceeds to `Create TEDS Enrichment`.
- **On Failure**:
  - Proceeds to `Create TEDS Error Enrichment`.
- **Details**:
  - **Inputs**:
    - `path_parameters`: Includes the UUID of the submitted observable.

---

## 6. Create TEDS Enrichment
- **Type**: `transformation`
- **Purpose**: Creates enriched metadata based on retrieved reputation data.
- **On Success**:
  - Proceeds to `Update Enrichment (Reputation)`.
- **Details**:
  - **Transformations**:
    - **Enrichment Verdict**: Categorizes observables as `unknown`, `Harmless`, `benign`, `suspicious`, or `malicious` based on URLScan scores.
    - **Enrichment Timestamp**: Captures the current timestamp.
    - **Enrichment Permalink**: Retrieves the permalink to the URLScan result.
    - **Enrichment Context**: Aggregates key details such as malicious verdicts, benign verdicts, categories, and the overall malicious status.

---

## 7. Create TEDS Error Enrichment
- **Type**: `connector`
- **Purpose**: Handles errors during enrichment by creating an error entry.
- **On Success**:
  - Proceeds to `Update Enrichment (Error: Reputation)`.
- **Details**:
  - **Inputs**:
    - `error_provider`: Set to `"URLScan"`.
    - `error_result`: Includes error details.

---

## 8. Update Enrichment (Reputation)
- **Type**: `updateVariables`
- **Purpose**: Updates the global `Enrichment` variable with reputation data.
- **Details**:
  - **Inputs**:
    - `Enrichment`: Populated with transformed enrichment data.

---

## 9. Update Enrichment (Error: Reputation)
- **Type**: `updateVariables`
- **Purpose**: Updates the global `Enrichment` variable with error details.
- **Details**:
  - **Inputs**:
    - `Enrichment`: Includes error details from `Create TEDS Error Enrichment`.

---

# Process Flow Summary

1. **Initialize Variables**:
   - The playbook starts by setting up the enrichment provider and observable value.
2. **Evaluate Observable Types**:
   - Determines if the observable is supported (e.g., IP, domain, URL).
3. **Submit Observable**:
   - Sends the observable to URLScan for analysis.
4. **Retrieve Reputation Data**:
   - Fetches reputation details and checks for errors.
5. **Generate Enrichment**:
   - Transforms retrieved data into a comprehensive enrichment entry.
6. **Handle Errors**:
   - Creates and logs error details if the enrichment fails.
7. **Update Enrichment Variable**:
   - Saves the enriched data or errors into the global `Enrichment` variable.

---

# Output

The playbook populates the `Enrichment` variable with structured data, including the enrichment type, verdict, timestamp, permalink, context, and raw data. In case of errors, the variable includes detailed error information.