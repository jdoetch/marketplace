# Overview

This component automates the enrichment of observables such as URLs, IP addresses, domains, and hashes using the Sekoia.io threat intelligence platform. It leverages a series of conditionals and transformations to retrieve reputation information, construct enrichment data, and manage errors when necessary. The component ensures consistency and actionable insights by integrating with Sekoia.io's APIs and performing structured transformations on the retrieved data.

# Actions Overview

## 1. Create Enrichment Variables
- **Type**: `createVariables`
- **Purpose**: Initializes the enrichment provider and an empty enrichment list.
- **On Success**: Proceeds to the `Conditional Parallel` action.
- **Details**:
  - **Inputs**:
    - `Enrichment_Provider`: Default value is `"Sekoia"`.
    - `Enrichment`: An empty list `[]`.

---

## 2. Conditional Parallel
- **Type**: `parallelGroup`
- **Purpose**: Distributes the workflow into different branches based on the observable type.
- **On Complete**: Executes the `NOOP` action.
- **Details**:
  - **Entrypoints**:
    - `IP_Address`
    - `Hash_Lookup_`
    - `Domain_Lookup`
    - `Url_Lookup`

---

### Branch 1: URL Lookup
#### 2.1. URL Lookup
- **Type**: `conditional`
- **Purpose**: Verifies if the observable type is `url`.
- **On Success**: Executes the `getIndicatorsByValue_avqmf` action.
- **Details**:
  - **Condition**:
    - Observable type matches `url`.

#### 2.2. Retrieve URL Indicators
- **Type**: `connector`
- **Purpose**: Fetches indicators associated with the URL observable from Sekoia.io.
- **On Success**: Proceeds to the `Create TEDS Enrichment URL Lookup` action.
- **On Failure**: Executes the `CreateTEDSErrorEnrichment_URL_Lookup` action.
- **Details**:
  - **Inputs**:
    - `parameters`: Contains the observable value and type (`url`).

#### 2.3. Create TEDS Enrichment URL Lookup
- **Type**: `transformation`
- **Purpose**: Constructs an enrichment entry with reputation data, including verdicts, timestamps, and context.
- **On Success**: Proceeds to the `Update Enrichment (URL)` action.
- **Details**:
  - **Transformations**:
    - `enrichment_verdict`: Categorizes the risk score into malicious or unknown.
    - `enrichment_timestamp`: Captures the modified timestamp or current time.
    - `enrichment_permalink`: Constructs a permalink to the Sekoia.io object.
    - `enrichment_context`: Builds a context string with confidence scores and MITRE ATT&CK tactics.

#### 2.4. Update Enrichment (URL)
- **Type**: `updateVariables`
- **Purpose**: Updates the global enrichment list with the newly created URL enrichment.
- **On Success**: Completes the branch.

#### 2.5. Create Error Enrichment for URL
- **Type**: `connector`
- **Purpose**: Handles errors during URL enrichment creation.
- **On Success**: Proceeds to `Update Enrichment (Error: URL)`.

#### 2.6. Update Enrichment (Error: URL)
- **Type**: `updateVariables`
- **Purpose**: Updates the global enrichment list with error data for the URL observable.

---

### Branch 2: Domain Lookup
Similar to the URL Lookup branch but tailored to domain observables.

---

### Branch 3: IP Address Lookup
Similar to the URL Lookup branch but tailored to IP address observables.

---

### Branch 4: Hash Lookup
Similar to the URL Lookup branch but tailored to hash observables (e.g., MD5, SHA1, SHA256).

---

## 3. NOOP
- **Type**: `transformation`
- **Purpose**: Acts as a placeholder to mark the completion of all branches.

---

# Process Flow Summary

1. **Initialization**:
   - The component begins by defining global variables for enrichment, including the provider and an empty enrichment list.

2. **Observable Type Handling**:
   - Based on the type of observable (URL, domain, IP address, or hash), the workflow branches into specific processing paths.

3. **Enrichment Creation**:
   - Retrieves indicators for the observable.
   - Constructs detailed enrichment entries, including verdicts, timestamps, permalinks, and contextual information.

4. **Error Handling**:
   - Captures and logs errors encountered during enrichment creation, ensuring visibility and traceability.

5. **Completion**:
   - Updates the global enrichment list with successful or error data and concludes the workflow.

---

# Output

The component outputs a global `Enrichment` variable containing processed data for observables, including reputation verdicts, contextual details, and raw data. This ensures actionable intelligence and comprehensive insights for end-users.