Component Documentation
Summary
This component begins by setting variables from provided inputs, then validates that certain conditions are met before creating a new indicator using a hash value. It transforms the input data into a suitable structure for CrowdStrike Falcon, creates a block hash indicator, optionally consolidates outputs, and finally updates the result variable. If the validation fails, it raises an error.

Actions and Their Purpose
Create Variables
Type: createVariables  
Purpose: Initializes variables including type, hash_value, expiration_days, and placeholders for result and ActionError.  
On success: Moves to Conditional_Parallel.

Conditional_Parallel
Type: parallelGroup  
Purpose: Validates input conditions and, if successful, transforms data and creates a block hash indicator. If validation fails, it stops execution.

Within Conditional_Parallel:

Input_Validation
Type: conditional  
Purpose: Checks if type and hash_value are not null. If valid, proceeds to Consolidate_Outputs after creating the block hash. If invalid, calls Input_Validation_Error.

Input_Validation_Error
Type: python  
Purpose: Raises a custom error if the input validation fails.  
No further actions since input validation failed.

Hash_Json_Data
Type: transformation  
Purpose: Transforms input variables into a structured JSON array suitable for CrowdStrike’s create_indicator action.  
On success: Calls Block_Hash.

Block_Hash
Type: connector  
Purpose: Uses CrowdStrike Falcon to create a new block hash indicator based on the transformed data.  
On success: Calls Consolidate_Outputs.

Consolidate_Outputs
Type: transformation  
Purpose: Transforms and consolidates the outputs, if necessary.  
On success: Calls Action_Error_Update.

Action_Error_Update
Type: updateVariables  
Purpose: Records that the action completed successfully.  
On success: Allows the process to continue back to Update_Result_Variable outside the parallel group.

Update_Result_Variable
Type: updateVariables  
Purpose: Updates the result variable with the consolidated outputs.  
On success: The component’s execution concludes.

Process Flow Summary
The component initializes variables and then validates the input. If the input fails validation, it raises an error and stops. If validation succeeds, it transforms the input data into a required format, creates an indicator with CrowdStrike Falcon, and consolidates the outputs. Finally, it updates the result variable. Throughout the process, errors and conditions are strictly handled, ensuring the component either completes successfully with a final structured result or terminates with a recorded error.