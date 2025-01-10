**Overview**
This playbook automates the process of handling `Domain` in response to specified actions (`block` or `unblock`). Depending on the action, it updates variables, interacts with a FortiGate firewall to add or remove `domain` from a designated network address group, and logs the result with timestamps.

**Actions Overview**
1. Global Variables
* Type: `createVariables`
* Purpose: Initializes a global variable `response_message` with a default value indicating a configuration error.
* On Success:
  - Proceeds to the `If_action_is_Block` action.
* On Failure: None.
* Details:
  - Default value of `response_message`: `"No response message available. Configuration error."`

2. If Action is Block
* Type: `conditional`
* Purpose: Evaluates whether the `action` input is `block`.
* On Success:
  - Proceeds to `execute_Fortigate_AddDomain`.
* On Failure: None.
 - Else: Redirects to `If_action_is_Unblock`.
Conditions:
* Checks if `action` equals `block` (case-insensitive).

3. Fortigate - Add Domain to Network Address Group
* Type: `connector`
* Purpose: Adds a `Domain` to the designated network address group i.e., "SWIMLANE_BLOCK_LIST" in the FortiGate firewall.
* On Success:
  - Fetches the current timestamp (`Get_Current_Timestamp`).
* Details:
* Inputs:
  - `Domain`: Derived from `{observable}`.
  - `Firewall_Address_Group_Name`: `"SWIMLANE_BLOCK_LIST"`

4. Get Current Timestamp
* Type: `transformation`
* Purpose: Fetches and formats the current timestamp in the Asia/Singapore timezone.
* On Success:
  - Updates variables (`updateVariables`).
Details:
  - Generates a formatted timestamp.

5. Update Variables (Post-Block)
* Type: `updateVariables`
* Purpose: Logs the success message for the block action with the timestamp.
Details:
  - Message Template: `"Domain {observable} has been added into Network Address Group at FortiGate, at {timestamp}."`

6. If Action is Unblock
* Type: `conditional`
* Purpose: Evaluates whether the `action` input is `unblock`.
* On Success:
  - Proceeds to `execute_Fortigate_RemoveDomain`.
* Else: Redirects to `No_VIC_Selected_Unknown_Action_Message`.
Conditions:
* Checks if `action` equals `unblock` (case-insensitive).

7. Fortigate - Remove Domain From Network Address Group
* Type: `connector`
* Purpose: Removes a `Domain` from the designated network address group i.e., "SWIMLANE_BLOCK_LIST" in the FortiGate firewall.
* On Success:
  - Fetches the current timestamp (`Get_Current_Timestamp_Unblock`).
* Details:
* Inputs:
  - `Domain`: Derived from `{observable}`.
  - `Firewall_Address_Group_Name`: `"SWIMLANE_BLOCK_LIST"`

8. Get Current Timestamp (Unblock)
* Type: `transformation`
* Purpose: Fetches and formats the current timestamp in the Asia/Singapore timezone.
* On Success:
  - Updates variables (`updateVariables`).
* Details:
  - Generates a formatted timestamp.

9. Update Variables (Post-Unblock)
* Type: `updateVariables`
* Purpose: Logs the success message for the unblock action with the timestamp.
* Details:
  - Message Template: `"Domain {observable} has been removed from Network Address Group at FortiGate, at {timestamp}."`

10. No VIC Selected Unknown Action Message
* Type: `updateVariables`
* Purpose: Logs an error message for unsupported actions.
* Details:
  - Message Template: `"Unknown action {action}. Configuration error."`

**Process Flow Summary**
1. **Initialize Variables**: The playbook starts by creating a `response_message` variable with a default error message.
2. **Action Evaluation**:
* If the action is `block`, it handles the block logic:
  - Logs a message and adds the Domain to the FortiGate group.
  - Captures a timestamp and logs the outcome.
* If the action is `unblock`, it handles the unblock logic:
  - Logs a message and removes the Domain from the FortiGate group.
  - Captures a timestamp and logs the outcome.
  - If the action is unsupported, it logs an error.
3. **Output**: The `response_message` variable is updated throughout the workflow to reflect the current status or errors.