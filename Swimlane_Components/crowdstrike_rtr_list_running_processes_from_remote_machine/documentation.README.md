# CrowdStrikeFalcon - RTR - Execute PS (Processes) and Return Results

## Actions and Their Purpose

### Component Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations. These include:
- ActionError: Tracks any errors that occur during execution.
- result: Stores the final output results.
- Host_Ids: References the input Host_ID.
- Command: Specifies the command to execute (ps).
- Wait_time: Sets the wait duration (10 seconds).

**On Success:** Proceeds to Get_Host_ID.

### Get_Host_ID
**Type:** transformation  
**Purpose:** Extracts the first host ID from the Host_Ids array provided in the input.

**On Success:** Calls Conditional_Parallel.

### Conditional_Parallel
**Type:** parallelGroup  
**Purpose:** Manages multiple conditional checks and subsequent actions simultaneously. It ensures that inputs are valid before proceeding with command execution.

**On Success:** Calls Get_Results.

#### Within Conditional_Parallel:

#### Input_Validation
**Type:** conditional  
**Purpose:** Validates that the extracted host_id meets the expected conditions required by downstream actions.

**Conditions:** 
- Checks if host_id is not equal to an unspecified value (e.g., not null or empty).

**Else:** Calls Input_Validation_Error.

#### Input_Validation_Error
**Type:** python  
**Purpose:** Executes a script to raise a custom error message when input validation fails.

**On Success:** Calls Update_Action_Error_Input_Validation.

#### Update_Action_Error_Input_Validation
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable with details from the Input_Validation_Error action.

#### Get_online_State
**Type:** http  
**Purpose:** Sends a GET request to CrowdStrike’s API to determine the online state of the host identified by host_id.

**On Success:** Calls initRTRSession.  
**On Failure:** Calls RaiseError.

#### RaiseError
**Type:** python  
**Purpose:** Executes a script to raise an error if any action fails after input validation.

**On Success:** Calls Update_Action_Error.

#### Update_Action_Error
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable with details from the error raised by RaiseError.

#### initRTRSession
**Type:** connector  
**Purpose:** Initiates a Real-Time Response (RTR) session with the host using the provided host_id.

**On Success:** Calls session_id.

#### session_id
**Type:** transformation  
**Purpose:** Extracts the session_id from the RTR session initiation response.

**On Success:** Calls executeRTRCommand.

#### executeRTRCommand
**Type:** connector  
**Purpose:** Executes the specified command (ps) on the host through the established RTR session.

**On Success:** Calls waitNSeconds.

#### waitNSeconds
**Type:** connector  
**Purpose:** Waits for a predefined number of seconds (Wait_time) before retrieving the command output.

**On Success:** Calls rTRCMDResult.

#### rTRCMDResult
**Type:** connector  
**Purpose:** Retrieves the results of the previously executed RTR command.

**On Success:** Calls command_results.

#### command_results
**Type:** transformation  
**Purpose:** Processes and structures the command’s output into a usable format.

**On Success:** Calls Action_Error_Update.

#### Action_Error_Update
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable to indicate the successful completion of actions.

### Get_Results
**Type:** transformation  
**Purpose:** Consolidates the online state of the host and the command’s standard output (stdout) into a final result object.

**On Success:** Calls Update_Result_Variable.

### Update_Result_Variable
**Type:** updateVariables  
**Purpose:** Updates the result variable with the consolidated results from Get_Results.

**On Success:** The component’s execution concludes successfully.

## Process Flow Summary

1. **Initialization:** The component begins by initializing necessary variables, including host identifiers and command details.
2. **Host ID Extraction:** It extracts a single host ID from the provided Host_Ids array.
3. **Conditional Parallel Processing:** 
   - **Input Validation:** Validates the extracted host ID. If invalid, it raises and records an error.
   - **Online State Check:** If valid, it queries CrowdStrike to determine the host’s online state.
4. **Error Handling:** If the online state check fails, an error is raised and recorded.
5. **RTR Session Management:** 
   - **Session Initialization:** If the host is online, it initializes an RTR session.
   - **Command Execution:** Executes the ps command on the host.
   - **Waiting Period:** Waits for 10 seconds to allow command execution to complete.
   - **Result Retrieval:** Retrieves the output of the executed command.
6. **Result Processing:** Processes and structures the command output.
7. **Finalization:** Consolidates all results and updates the result variable, concluding the component successfully.
8. **Error Recording:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final results stored in the result variable.