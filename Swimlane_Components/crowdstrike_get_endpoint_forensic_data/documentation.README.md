Component Documentation
Summary
This component initializes necessary variables, extracts a host identifier, and performs a series of actions to validate the input, determine the host’s online state through CrowdStrike, establish a session for remote commands, execute commands to retrieve netstat and process lists, and finally present a consolidated set of results. If at any step an issue occurs, the component records the error details for troubleshooting.

Actions and Their Purpose
Create Variables
Type: createVariables  
Purpose: Initializes the environment, including variables for action errors, results, and host identifiers.  
On success: Moves to Get_Host_ID.

Get_Host_ID
Type: transformation  
Purpose: Extracts a single host identifier from the provided array. This host identifier will be used by downstream actions.  
On success: Moves to Conditional_Parallel.

Conditional_Parallel
Type: parallelGroup  
Purpose: Runs multiple actions in parallel to validate input and, if valid, proceed with retrieving the host’s online state, setting up a remote session, and executing remote commands.  
On success: Moves to Get_Results.

Within Conditional_Parallel:

Input_Validation
Type: conditional  
Purpose: Checks if the extracted host identifier meets expected criteria.  
If validation fails, calls Input_Validation_Error.

Input_Validation_Error
Type: python  
Purpose: Raises an error when input validation fails.  
On success: Calls Update_Action_Error_Input_Validation.

Update_Action_Error_Input_Validation
Type: updateVariables  
Purpose: Updates the ActionError variable with details from the Input_Validation_Error result.  
On success: Stops further progress since input validation failed.

Get_online_State
Type: http  
Purpose: Uses a CrowdStrike endpoint to determine the host’s online state.  
On success: Calls initializeRTRSession to start a remote session.  
On failure: Calls RaiseError.

initializeRTRSession
Type: connector  
Purpose: Initiates a real-time response session with the host.  
On success: Calls session_id transformation to extract the session identifier.

session_id
Type: transformation  
Purpose: Extracts the session ID from the session initialization results.  
On success: Calls parallel_adkdt.

parallel_adkdt
Type: parallelGroup  
Purpose: Runs multiple commands (netstat and ps) in parallel on the host via the established session. Each command waits for a short period before retrieving its output.  
On success: Calls command_results transformation.

Within parallel_adkdt:

Execute_Netstat
Type: connector  
Purpose: Executes a netstat command on the host.  
On success: Calls waitNSeconds_a1u6e to delay before retrieving output.

waitNSeconds_a1u6e
Type: connector  
Purpose: Waits a specified number of seconds before retrieving netstat command output.  
On success: Calls Netstat_stdout.

Netstat_stdout
Type: connector  
Purpose: Retrieves the output of the previously run netstat command.  
On success: Results are used downstream.

Execute_PS
Type: connector  
Purpose: Executes a ps command on the host.  
On success: Calls waitNSeconds_a0qu1.

waitNSeconds_a0qu1
Type: connector  
Purpose: Waits a specified number of seconds before retrieving ps command output.  
On success: Calls Processes_stdout.

Processes_stdout
Type: connector  
Purpose: Retrieves the output of the previously run ps command.  
On success: Results are used downstream.

command_results
Type: transformation  
Purpose: Transforms both netstat and ps command outputs into a structured format.  
On success: Calls Action_Error_Update.

Action_Error_Update
Type: updateVariables  
Purpose: Updates the ActionError variable to indicate that the action completed successfully.  
On success: Allows the flow to continue.

RaiseError
Type: python  
Purpose: Raises an error if any action fails during retrieval or processing.  
On success: Calls Update_Action_Error.

Update_Action_Error
Type: updateVariables  
Purpose: Updates ActionError with details from RaiseError.  
On success: No further progress due to error.

Post-Parallel Actions
Get_Results
Type: transformation  
Purpose: Consolidates the results of the host’s online state check, netstat output, and ps output into a single structured result.  
On success: Calls Update_Result_Variable.

Update_Result_Variable
Type: updateVariables  
Purpose: Stores the transformed results in the result variable for review or further processing.  
On success: The component concludes successfully.

Overall Process Flow Summary
The component begins by creating and defining variables. It selects a single host identifier, then validates the input. If validation fails, an error is recorded and no further actions are taken. If validation is successful, it retrieves the host’s online state from CrowdStrike, establishes a remote session, and executes multiple remote commands to gather host information.

After executing these commands, the component waits briefly, then retrieves their outputs. It transforms these outputs into a structured format and updates variables to reflect the state of actions and results. Finally, it produces a consolidated result showing the host’s online state and the output of the executed commands. If at any point a failure occurs, the component records the error details and stops processing. This ensures that both successful and failing conditions are well-documented and actionable.