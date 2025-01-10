Summary

This component is designed to retrieve a host identifier, validate it, check the host’s online state using CrowdStrike, establish a real-time response (RTR) session, execute a command (ls c:\\windows\\prefetch), wait for a specified duration, retrieve the command output, and finally compile the results. Throughout the process, it handles errors by raising and recording them appropriately. Upon successful execution, it outputs the host’s online state and the command’s results.

Actions and Their Purpose
Component Variables
Type: createVariables  
Purpose: Initializes essential variables, including ActionError, result, Host_Ids, Command (set to ls c:\\windows\\prefetch), Wait_time (set to 10 seconds), and username.  
On Success: Proceeds to Get_Host_ID.

Get_Host_ID
Type: transformation  
Purpose: Extracts the first host ID from the Host_Ids array.  
On Success: Calls Conditional_Parallel.

Conditional_Parallel
Type: parallelGroup  
Purpose: Handles multiple conditionals simultaneously. It begins with input validation to ensure that the host ID is valid before proceeding with further actions.  
On Success: Calls Get_Results.

Within Conditional_Parallel:
Input_Validation
Type: conditional  
Purpose: Validates that the extracted host_id meets the expected conditions. If the validation fails, it triggers an error handling sequence.  
Conditions: Checks if host_id is not equal to a specified value (e.g., not null or empty).  
Else: Calls Input_Validation_Error.

Input_Validation_Error
Type: python  
Purpose: Executes a script to raise a custom error message when input validation fails.  
On Success: Calls Update_Action_Error_Input_Validation.

Update_Action_Error_Input_Validation
Type: updateVariables  
Purpose: Updates the ActionError variable with the error details from Input_Validation_Error.

Get_online_State
Type: http  
Purpose: Sends a GET request to CrowdStrike’s API to determine the online state of the host identified by host_id.  
On Success: Calls initRTRSession to initiate a real-time response session.  
On Failure: Calls RaiseError.

RaiseError
Type: python  
Purpose: Executes a script to raise an error if any action fails after validation.  
On Success: Calls Update_Action_Error.

Update_Action_Error
Type: updateVariables  
Purpose: Updates the ActionError variable with details from the error raised by RaiseError.

initRTRSession
Type: connector  
Purpose: Initiates a real-time response (RTR) session with the host using the provided host_id.  
On Success: Calls session_id to process the session details.

session_id
Type: transformation  
Purpose: Extracts the session_id from the RTR session initiation response.  
On Success: Calls executeRTRCommand.

executeRTRCommand
Type: connector  
Purpose: Executes the specified command (ls c:\\windows\\prefetch) on the host through the established RTR session.  
On Success: Calls waitNSeconds.

waitNSeconds
Type: connector  
Purpose: Waits for a predefined number of seconds (Wait_time) before proceeding to retrieve command output.  
On Success: Calls rTRCMDResult.

rTRCMDResult
Type: connector  
Purpose: Retrieves the results of the previously executed RTR command (ls c:\\windows\\prefetch).  
On Success: Calls command_results.

command_results
Type: transformation  
Purpose: Processes and structures the command’s output for further use.  
On Success: Calls Action_Error_Update.

Action_Error_Update
Type: updateVariables  
Purpose: Updates the ActionError variable to indicate the successful completion of the actions.

Get_Results
Type: transformation  
Purpose: Consolidates the host’s online state and the command’s standard output (stdout) into a final result object.  
On Success: Calls Update_Result_Variable.

Update_Result_Variable
Type: updateVariables  
Purpose: Updates the result variable with the consolidated results from Get_Results.  
On Success: The component’s execution concludes successfully.

Process Flow Summary

Initialization: The component starts by initializing necessary variables, including host identifiers, commands, and error tracking.

Host ID Extraction: It extracts a single host ID from the provided Host_Ids array.

Conditional Parallel Processing: 

Input Validation: Validates the extracted host ID. If invalid, it raises and records an error.

Online State Check: If valid, it queries CrowdStrike to determine the host’s online state.

Error Handling: If the online state check fails, an error is raised and recorded.

RTR Session Management: 

Session Initialization: If the host is online, it initializes an RTR session.

Command Execution: Executes the ls c:\\windows\\prefetch command on the host.

Waiting Period: Waits for a specified duration to allow command execution to complete.

Result Retrieval: Retrieves the output of the executed command.

Result Processing: Processes and structures the command output.

Finalization: Consolidates all results and updates the result variable, concluding the component successfully.

Error Recording: At any point of failure, the component raises and records errors, ensuring that issues are tracked appropriately.