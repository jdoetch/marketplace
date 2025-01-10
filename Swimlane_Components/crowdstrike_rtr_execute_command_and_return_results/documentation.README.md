Summary
This component initializes variables, retrieves a host identifier, validates the input against expected criteria, determines the host’s online state through a CrowdStrike endpoint, initializes a remote session, executes a specified command on the host, waits, retrieves command results, and finally transforms and presents these results. In case of errors at any stage, the component records the details, ensuring visibility into any failures.

Actions and Their Purpose
Component_Variables
Type: createVariables  
Purpose: Sets up the initial environment by defining variables such as the host identifier, command to execute, and other placeholders.  
On success: Proceeds to Get_Host_ID.

Get_Host_ID
Type: transformation  
Purpose: Extracts a single host identifier from the provided input array for subsequent actions to use.  
On success: Moves to Conditional_Parallel.

Conditional_Parallel
Type: parallelGroup  
Purpose: Evaluates conditions and, if successful, continues with actions to retrieve host state, initialize a remote session, execute a command, and handle results. If validation fails, it records the error and stops.

Within Conditional_Parallel:

Input_Validation
Type: conditional  
Purpose: Checks if the extracted host identifier meets the criteria expected by downstream actions.  
If invalid, calls Input_Validation_Error.

Input_Validation_Error
Type: python  
Purpose: Raises a custom error if input validation fails.  
On success: Calls Update_Action_Error_Input_Validation.

Update_Action_Error_Input_Validation
Type: updateVariables  
Purpose: Records the error from Input_Validation_Error into the ActionError variable.  
No further actions since validation failed.

Get_online_State
Type: http  
Purpose: Queries CrowdStrike to determine if the host is online.  
On success: Calls initRTRSession to start a remote session.  
On failure: Calls RaiseError.

initRTRSession
Type: connector  
Purpose: Initializes a real-time response session with the host to enable command execution.  
On success: Calls session_id.

session_id
Type: transformation  
Purpose: Extracts the session ID created by initRTRSession for the next steps.  
On success: Calls executeRTRCommand.

executeRTRCommand
Type: connector  
Purpose: Executes the specified command on the remote host session.  
On success: Calls waitNSeconds to delay before retrieving the command results.

waitNSeconds
Type: connector  
Purpose: Waits a predefined number of seconds before retrieving the command’s output.  
On success: Calls rTRCMDResult.

rTRCMDResult
Type: connector  
Purpose: Retrieves the results of the executed command.  
On success: Calls command_results.

command_results
Type: transformation  
Purpose: Processes and structures the command’s output.  
On success: Calls Action_Error_Update.

Action_Error_Update
Type: updateVariables  
Purpose: Indicates successful action completion by updating the ActionError variable.  
No further actions needed for this branch.

RaiseError
Type: python  
Purpose: Raises an error if any step fails after validation.  
On success: Calls Update_Action_Error.

Update_Action_Error
Type: updateVariables  
Purpose: Records the error details raised by RaiseError into ActionError.  
No further progress since an error occurred.

Get_Results
Type: transformation  
Purpose: Consolidates the host’s online state and the command’s stdout into a final structured result.  
On success: Calls Update_Result_Variable.

Update_Result_Variable
Type: updateVariables  
Purpose: Stores the transformed result into the result variable, completing the component’s process.  
No further actions required.

Process Flow Summary
The component begins by setting up variables and extracting a single host identifier. It then enters a conditional phase where the input is validated. If input validation fails, it logs the error and stops. If it succeeds, the component retrieves the host’s online state, sets up a remote session, executes a command on the host, waits, retrieves the command’s output, and processes these outputs into a structured result.

If at any point an action fails, the component records an error in ActionError and does not proceed further. On successful completion, it provides a final set of results ready for review or further action.