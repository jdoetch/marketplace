# Component: `zscaler_block_unblock_url_remediation_action`

## Overview

The `zscaler_block_unblock_url_remediation_action` automates the process of managing URL blacklisting and unblocking in Zscaler. It ensures efficient handling of malicious or unwanted URLs as part of a broader incident response strategy. This component evaluates the provided action (`block` or `unblock`), applies the appropriate logic, and returns a status message reflecting the outcome.

---

## Actions Overview

### 1. **Global Variables**
   - **Type**: Create Variables
   - **Purpose**: Initializes the variable `response_message` with a default message:  
     `"No response message available. Configuration error."`
   - **On-Success**: Proceeds to evaluate whether the action is `block` or `unblock`.

---

### 2. **If Action is Block**
   - **Type**: Conditional
   - **Purpose**: Evaluates whether the requested action is `block`. If true, it triggers the `Block_URL` action.
   - **Conditions**:
     - The input action is `block` (case-insensitive match).
   - **Else**: Redirects to `If Action is Unblock`.

---

### 3. **If Action is Unblock**
   - **Type**: Conditional
   - **Purpose**: Evaluates whether the requested action is `unblock`. If true, it triggers the `Unblock_URL` action.
   - **Conditions**:
     - The input action is `unblock` (case-insensitive match).
   - **Else**: Redirects to `No VIC Selected Unknown Action Message`.

---

### 4. **No VIC Selected Unknown Action Message**
   - **Type**: Update Variables
   - **Purpose**: Sets a default error message if the action is neither `block` nor `unblock`.  
     Message: `"Unknown action {action}. Configuration error."`

---

### 5. **Block URL**
   - **Type**: Connector
   - **Purpose**: Adds a specified URL to Zscaler's blacklist.
   - **Inputs**:
     - **Action**: `ADD_TO_LIST`
     - **URL(s)**: `{observable}` (passed dynamically).
     - **SSL Verification**: Enabled.
   - **On-Success**: Triggers `Block_Message`.

---

### 6. **Unblock URL**
   - **Type**: Connector
   - **Purpose**: Removes a specified URL from Zscaler's blacklist.
   - **Inputs**:
     - **Action**: `REMOVE_FROM_LIST`
     - **URL(s)**: `{observable}` (passed dynamically).
   - **On-Success**: Triggers `Unblock_Message`.

---

### 7. **Block Message**
   - **Type**: Update Variables
   - **Purpose**: Updates the response message to confirm a URL has been blocked.
   - **Message**:  
     `"Observable {observable} is blocked."`

---

### 8. **Unblock Message**
   - **Type**: Update Variables
   - **Purpose**: Updates the response message to confirm a URL has been unblocked.
   - **Message**:  
     `"Observable {observable} is unblocked."`

---

## Process Flow Summary

1. The component initializes with global variables, setting a default response message.
2. Based on the input `action`:
   - If the action is `block`, the `Block_URL` process is triggered:
     - The specified URL is added to Zscaler's blacklist.
     - A confirmation message is generated.
   - If the action is `unblock`, the `Unblock_URL` process is triggered:
     - The specified URL is removed from Zscaler's blacklist.
     - A confirmation message is generated.
   - If the action is neither `block` nor `unblock`, a default error message is set.
3. The component outputs a `response_message` reflecting the outcome of the action.

---

## Inputs

- **observable**: The URL to be blocked or unblocked. *(Required)*  
- **observable_type**: The type of observable (e.g., URL). *(Required)*  
- **action**: Specifies the action (`block` or `unblock`). *(Required)*

---

## Outputs

- **response_message**: A string summarizing the result of the action (e.g., success or error message).