**Overview**
This automation playbook is designed to manage the isolation and rejoining of agents(Host ID) in a SentinelOne Endpoint Detection and Response (EDR) system based on a specified action input (`isolate` or `rejoin`). Here's a breakdown of its functionality:

**Actions Overview**
1. Initialize Variables
    * Action: `Create_Global_Variables`
    * Purpose: Initializes a global variable `response_message` with the default value:
      - `"No response available. Configuration Error."`
      - This serves as a fallback message for unexpected or unhandled situations.

2. Action Decision Based on Input
    * Action: `If_Action_Isolate`
        - If the input action is `isolate` (case-insensitive):
        - → Proceeds to isolate the specified agent using `S1_Disconnect_Agents`.
        - Otherwise:
        - → Routes the flow to `If_Action_Rejoin`.
    * Action: `If_Action_Rejoin`
        - If the input action is `rejoin` (case-insensitive):
        - → Proceeds to reconnect the specified agent using `S1_Connect_Agents`.
        - Otherwise:
        - → Updates `response_message` to indicate an unknown action using `No_VIC_Selected_Unknown_Action_Message`.

3. Isolate Agent
    * Action: `S1_Disconnect_Agents`
        - Sends a command to SentinelOne to disconnect the specified agent from the network.
        - On success: Moves to `Get_Current_Timestamp_Isolate`.

    * Action: `Get_Current_Timestamp_Isolate`
        - Fetches the current timestamp in the Asia/Singapore timezone.
        - On success: Moves to `updateVariables_block`.

    * Action: `updateVariables_block`
        - Updates `response_message` with a success message, e.g.,
        - `"Agent {host} has been Disconnect from Network at S1 EDR, at {current_timestamp}"`.

4. Rejoin Agent

    * Action: `S1_Connect_Agents`
        - Sends a command to SentinelOne to reconnect the specified agent to the network.
        - On success: Moves to `Get_Current_Timestamp_Rejoin`.

    * Action: `Get_Current_Timestamp_Rejoin`
        - Fetches the current timestamp in the Asia/Singapore timezone.
        - On success: Moves to `updateVariables_unblock`.

    * Action: `updateVariables_unblock`
        - Updates `response_message` with a success message, e.g.,
        - `"Agent {host} has been Reconnected to Network at S1 EDR, at {current_timestamp}"`.

5. Handle Unknown Actions

    * Action: `No_VIC_Selected_Unknown_Action_Message`
        - Updates `response_message` with an error message, e.g.,
        - `"Unknown action {action}. Configuration error."`

**Inputs and Outputs**
    * Inputs:
        - `host` (string): Specifies the host ID of the agent to be acted upon.
        - `action` (string): Defines the action (isolate or rejoin).

    * Outputs:
        - `response_message` (string): Provides the result or error message of the playbook execution.

**Key Features**
    * **Conditional Logic**: Determines the appropriate path based on the `action` input.
    * **Integration with SentinelOne**: Uses SentinelOne API actions (`disconnect_agents` and `connect_agents`) for agent control.
    * **Timestamp Handling**: Ensures event logs include a timestamp in a specific timezone.
    * **Error Handling**: Manages unknown or invalid actions gracefully by providing meaningful feedback.

This playbook ensures that agents are efficiently isolated or rejoined while maintaining a clear audit trail through `response_message`.