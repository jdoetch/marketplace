# Component Documentation: `HarfangLab Isolate Rejoin Host Remediation Action Component`

## Overview

This component enables host isolation or rejoining within a security environment. It dynamically processes actions based on input, allowing for operational flexibility. The component handles two primary actions: isolating and rejoining hosts, ensuring detailed error handling and feedback.

---

## Actions Overview

### 1. **Create Global Variables**
   - **Type**: `createVariables`
   - **Purpose**: Initializes the `response_message` variable with a default value to manage errors and feedback.
   - **Inputs**:
     - `response_message`: Default message indicating a configuration error.
   - **Next Steps**:
     - **On-Success**: `If Action Isolate`

---

### 2. **If Action Isolate**
   - **Type**: `conditional`
   - **Purpose**: Determines if the action input is set to "isolate."
   - **Condition**:
     - Checks if the `action` input matches `isolate` (case-insensitive).
   - **Next Steps**:
     - **On-Success**: Proceeds to `Endpoint Search` for isolation.
     - **On-Failure**: Redirects to `If Action Rejoin`.

---

### 3. **Endpoint Search**
   - **Type**: `connector`
   - **Purpose**: Searches for the endpoint corresponding to the provided host.
   - **Inputs**:
     - `hostname`: Hostname provided in the `host` input.
   - **Next Steps**:
     - **On-Success**: Executes `Isolate Host`.

---

### 4. **Isolate Host**
   - **Type**: `http`
   - **Purpose**: Sends an HTTP request to isolate the specified host.
   - **Inputs**:
     - `endpoint`: API endpoint for host isolation, dynamically constructed using the search results.
   - **Next Steps**:
     - **On-Success**: Evaluates response in `If OK`.
     - **On-Failure**: Logs error.

---

### 5. **If OK**
   - **Type**: `conditional`
   - **Purpose**: Checks the HTTP response status to determine isolation success.
   - **Condition**:
     - Verifies if the response `status_code` equals `200`.
   - **Next Steps**:
     - **On-Success**: Updates the `response_message` via `No VIC Selected Isolate Message`.
     - **On-Failure**: Redirects to `Isolate Error Message`.

---

### 6. **Isolate Error Message**
   - **Type**: `updateVariables`
   - **Purpose**: Updates the `response_message` variable to indicate isolation failure.
   - **Inputs**:
     - `response_message`: "Error: Host {host} is not Isolated."

---

### 7. **If Action Rejoin**
   - **Type**: `conditional`
   - **Purpose**: Determines if the action input is set to "rejoin."
   - **Condition**:
     - Checks if the `action` input matches `rejoin` (case-insensitive).
   - **Next Steps**:
     - **On-Success**: Proceeds to `EndPoint Search` for rejoining.
     - **On-Failure**: Redirects to `No VIC Selected Unknown Action Message`.

---

### 8. **EndPoint Search**
   - **Type**: `connector`
   - **Purpose**: Searches for the endpoint corresponding to the provided host for rejoining.
   - **Inputs**:
     - `hostname`: Hostname provided in the `host` input.
   - **Next Steps**:
     - **On-Success**: Executes `Deisolate Host`.

---

### 9. **Deisolate Host**
   - **Type**: `http`
   - **Purpose**: Sends an HTTP request to rejoin the specified host.
   - **Inputs**:
     - `endpoint`: API endpoint for host rejoining, dynamically constructed using the search results.
   - **Next Steps**:
     - **On-Success**: Evaluates response in `if OK`.
     - **On-Failure**: Logs error.

---

### 10. **if OK**
   - **Type**: `conditional`
   - **Purpose**: Checks the HTTP response status to determine rejoining success.
   - **Condition**:
     - Verifies if the response `status_code` equals `200`.
   - **Next Steps**:
     - **On-Success**: Updates the `response_message` via `No VIC Selected Rejoin Message`.
     - **On-Failure**: Redirects to `Deisolate Error Message`.

---

### 11. **Deisolate Error Message**
   - **Type**: `updateVariables`
   - **Purpose**: Updates the `response_message` variable to indicate rejoining failure.
   - **Inputs**:
     - `response_message`: "Error: Host {host} not rejoined."

---

### 12. **No VIC Selected Isolate Message**
   - **Type**: `updateVariables`
   - **Purpose**: Updates the `response_message` variable to indicate successful isolation.
   - **Inputs**:
     - `response_message`: "Host {host} isolated."

---

### 13. **No VIC Selected Rejoin Message**
   - **Type**: `updateVariables`
   - **Purpose**: Updates the `response_message` variable to indicate successful rejoining.
   - **Inputs**:
     - `response_message`: "Host {host} rejoined."

---

### 14. **No VIC Selected Unknown Action Message**
   - **Type**: `updateVariables`
   - **Purpose**: Updates the `response_message` variable to indicate an unknown action.
   - **Inputs**:
     - `response_message`: "Unknown action {action}. Configuration error."

---

## Process Flow Summary

1. **Initialization**: The `Create Global Variables` action initializes the `response_message` variable.
2. **Action Determination**: 
   - `If Action Isolate` checks if the action is `isolate`.
   - If not, `If Action Rejoin` checks for `rejoin`.
3. **Endpoint Search**: Retrieves endpoint details for the specified host.
4. **Execution**:
   - If `isolate`, proceeds to isolate the host.
   - If `rejoin`, proceeds to rejoin the host.
5. **Validation**:
   - Validates the HTTP response via `If OK`.
   - Updates the `response_message` variable based on success or failure.
6. **Error Handling**: Logs errors or unknown actions to ensure transparency.

This component efficiently handles host isolation and rejoining processes with robust error management and clear feedback mechanisms.