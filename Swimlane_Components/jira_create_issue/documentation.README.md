## Summary

This component handles the creation of Jira issues. It begins by setting up variables, checking if only fields should be used directly or if reporter and assignee details should be validated and fetched. It then proceeds through conditional checks and transformations to assemble the correct set of fields for the Jira issue creation. If required, it retrieves user IDs for the reporter and assignee. Based on the conditions, it either creates an issue using a standard set of fields or directly uses a provided fields object. Finally, it updates variables with the newly created issue details.

## Actions and Their Purpose

### Jira_Create_Issue_Variables
Type: createVariables  
Purpose: Initializes variables including raw_json, ticket_key, and ticket_url placeholders. Sets up the environment for subsequent steps.  
On success: Calls Check_For_Fields_JSON.

### Check_For_Fields_JSON
Type: conditional  
Purpose: Checks if only fields should be used. If not, it proceeds to Check_For_Reporter_and_Assignee to validate and retrieve reporter and assignee details. If only fields are to be used, it calls Create_Issue_With_Custom_Fie.  
On success if conditions met: Calls Check_For_Reporter_and_Assignee.  
Else: Calls Create_Issue_With_Custom_Fie.

### Check_For_Reporter_and_Assignee
Type: transformation  
Purpose: Determines if reporter or assignee are empty using dynamic checks.  
On success: Calls parallel_ahajv.

### parallel_ahajv
Type: parallelGroup  
Purpose: Runs two conditional checks in parallel: one for reporter and one for assignee. If the reporter is not empty, it retrieves the reporter's ID. If the assignee is not empty, it retrieves the assignee's ID.  
On success: Calls Fields to transform fields for the issue.

Within parallel_ahajv:

#### Check_For_Reporter
Type: conditional  
Purpose: If the reporter is not empty, calls jira_GetUserIDByNameOrEmail_al4eu to retrieve the user ID.  
On success: No subsequent steps within this conditional.

#### jira_GetUserIDByNameOrEmail_al4eu
Type: connector  
Purpose: Retrieves the reporter's user ID based on name or email.  
On success: The result is used by Fields transformation.

#### Check_For_Assignee
Type: conditional  
Purpose: If the assignee is not empty, calls Get_Assignee to retrieve the user ID.  
On success: No subsequent steps within this conditional.

#### Get_Assignee
Type: connector  
Purpose: Retrieves the assignee's user ID based on name or email.  
On success: The result is used by Fields transformation.

### Fields
Type: transformation  
Purpose: Builds a combined set of standard fields (project, summary, issue type) and optionally includes reporter and assignee if they were not empty. It also merges these standard fields with any additional fields provided.  
On success: Calls Combine_Fields.

Within Fields transformation steps:

#### standard_fields
Uses inputs like project_key, summary, and IssueType_ID to build a base fields object. If reporter and assignee IDs were retrieved, it includes them as well.

#### fields
Merges standard_fields with additional fields from inputs.fields if provided.

### Combine_Fields
Type: python  
Purpose: Merges standard fields with additional fields into a single fields object.  
On success: Calls Create_Issue_With_Standard_Fields.

### Create_Issue_With_Standard_Fields
Type: connector  
Purpose: Creates a Jira issue using the merged standard and additional fields.  
On success: Calls Update_Vars_With_Standard_Fields.

### Update_Vars_With_Standard_Fields
Type: updateVariables  
Purpose: Updates variables raw_json, ticket_key, and ticket_url with data from the newly created Jira issue.  
On success: The process ends successfully.

### Create_Issue_With_Custom_Fie
Type: connector  
Purpose: Creates a Jira issue directly using the fields object provided in the input without adding standard fields.  
On success: Calls Update_Vars_Using_Fields.

### Update_Vars_Using_Fields
Type: updateVariables  
Purpose: Updates variables raw_json, ticket_key, and ticket_url with data from the newly created Jira issue when only fields were used.  
On success: The process ends successfully.

### Input_Validation_Error (If triggered)
Type: python  
Purpose: Raises an error if the initial validation fails (for example, if reporter or assignee is unexpectedly empty when required).  
On success: The process ends, as no further actions are taken.

## Process Flow Summary

1. The component starts by creating initial variables.  
2. It checks if only fields should be used. If so, it creates the issue using these fields and updates variables with the result.  
3. If not using only fields, it evaluates reporter and assignee inputs. If they are provided, it retrieves their user IDs in parallel.  
4. After collecting user IDs, it constructs standard fields along with any additional fields.  
5. It merges and creates a Jira issue with these fields.  
6. Finally, it updates variables with the newly created issue information.

If at any point conditions fail or validation fails, the component raises an error and stops. Otherwise, it completes successfully with a newly created Jira issue and updated variables reflecting the issue details.