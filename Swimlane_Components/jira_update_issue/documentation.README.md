# Jira - Update Issue

## Short Description

This component enables seamless updates to Jira issues by automating the modification of various fields such as reporter, assignee, summary, and description. It ensures that issue updates are performed accurately and efficiently by validating inputs, transforming data as needed, and handling errors gracefully. This enhances the incident management and tracking capabilities within Jira, streamlining the workflow for security and IT teams.

### Summary

The **Jira - Update Issue** component automates the process of updating Jira issues with specified fields. The workflow begins by initializing necessary variables, including the issue key and fields to be updated. It then validates the input to ensure that required fields are provided. If validation passes, the component proceeds to transform and combine the provided fields, such as reporter and assignee, into the appropriate JSON format required by Jira's API. It then performs the update operation on the specified Jira issue. Throughout the process, comprehensive error handling mechanisms are in place to capture and record any issues, ensuring reliable and efficient updates to Jira issues.

## Actions and Their Purpose

### Edit Issue Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations. These include:
- url: The Jira API URL endpoint.
- raw_json: Raw JSON data for the issue update.
- output_response: Stores the response from the Jira API after updating the issue.
- output_fields_json: Stores the transformed fields in JSON format.

**On Success:** Proceeds to Check_For_Fields_JSON.

### Check For Fields JSON
**Type:** conditional  
**Purpose:** Validates that the input fields meet the expected conditions required by downstream actions.

**Conditions:** 
- Checks if Incident_id is not equal to null.

**Else:** Calls Update_Issue.

### Input Validation Error
**Type:** python  
**Purpose:** Executes a script to raise a custom error message when input validation fails.

**On Success:** Calls updateVariables_a9aj2.

**Inputs:**
- errorRaised: true

### updateVariables_a9aj2
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable with details from the Input_Validation_Error action.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** actions.Input_Validation_Error.result

### Action_Error_Update
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable to indicate the successful completion of actions.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** Action Completed

### Action_Error
**Type:** python  
**Purpose:** Executes a script to raise an error if the Query_Detections_by_Incident_ID action fails.

**On Success:** Calls Update_Action_Error.

**Inputs:**
- errorRaised: true

### Update_Action_Error
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable with details from the Action_Error action.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** actions.Action_Error.result

### Query_Detections_by_Incident_ID
**Type:** connector  
**Purpose:** Queries Jira to retrieve detections associated with the specified incident ID.

**On Success:** Calls Get_Detection_Summaries.  
**On Failure:** Calls Action_Error.

**Inputs:**
- parameters:
  - q: References the Incident_id variable.
- verify_ssl: true

### Get_Detection_Summaries
**Type:** connector  
**Purpose:** Retrieves summaries of the detections obtained from the Query_Detections_by_Incident_ID action.

**On Success:** Calls Action_Error_Update.  
**On Failure:** No specific failure actions.

**Inputs:**
- json_body:
  - ids: References the resources from the Query_Detections_by_Incident_ID action result.
- verify_ssl: true

### Fields
**Type:** transformation  
**Purpose:** Prepares the standard fields required for updating the Jira issue.

**On Success:** Calls combine_fields.

**Transformations:**
- **standard_fields:**
  - **Expression:** {"summary" : inputs.summary}
  - **Data:** References the summary input.

### combine_fields
**Type:** python  
**Purpose:** Combines standard fields with additional fields such as reporter, assignee, and description into a single JSON object for the Jira API.

**On Success:** Calls Edit_Issue_With_Standard_Fields.

**Inputs:**
- standard_fields: References the Fields.result.standard_fields.
- additional_fields:
  - reporter: References the Create_Reporter_Json.result.reporter_json.
  - assignee: References the Create_Assignee_Json.result.assignee_json.
  - other_fields: References the inputs.fields.
  - description: References the Create_Description_Json.result.description_json.

### Edit_Issue_With_Standard_Fields
**Type:** connector  
**Purpose:** Sends the combined fields to Jira to update the specified issue.

**On Success:** Calls Update_Issue_Variables.  
**On Failure:** No specific failure actions.

**Inputs:**
- path_parameters: 
  - issueIdOrKey: References the issue_key input.
- json_body: References the combine_fields.result.

### Update_Issue_Variables
**Type:** updateVariables  
**Purpose:** Updates variables with the response from the Jira API after updating the issue.

**Inputs:**
- output_response:
  - **Operation:** set
  - **Value:** actions.Edit_Issue_With_Standard_Fields.result
- output_fields_json:
  - **Operation:** set
  - **Value:** actions.combine_fields.result

### Update_Issue
**Type:** connector  
**Purpose:** Updates the Jira issue with the provided fields.

**On Success:** Calls Update_Variables.  
**On Failure:** No specific failure actions.

**Inputs:**
- path_parameters: 
  - issueIdOrKey: References the issue_key input.
- json_body: References the fields input.

### Update_Variables
**Type:** updateVariables  
**Purpose:** Updates variables with the response from the Jira API after updating the issue.

**Inputs:**
- output_response:
  - **Operation:** set
  - **Value:** actions.Update_Issue.result
- output_fields_json:
  - **Operation:** set
  - **Value:** actions.fields.result

## Process Flow Summary

1. **Initialization:** The component begins by initializing necessary variables, including the Jira issue key, fields to be updated, and error tracking.
2. **Input Validation:** It validates the provided Incident_id to ensure it meets the expected conditions.
   - If invalid, it raises and records an error.
   - If valid, it proceeds to extract the host ID from the incident ID.
3. **Host ID Extraction:** Extracts the host ID from the provided incident ID.
4. **Vulnerability Search:** Executes a vulnerability search using Jira's API based on the extracted host ID.
   - If the search fails, it raises and records an error.
   - If successful, it retrieves and processes detection summaries.
5. **Field Preparation:** Prepares and combines standard fields with additional fields such as reporter, assignee, and description.
6. **Issue Update:** Sends the combined fields to Jira to update the specified issue.
   - If the update is successful, it records the response.
   - If the update fails, it raises and records an error.
7. **Result Consolidation:** Consolidates the detection summaries and update responses into the result variable.
8. **Finalization:** Updates the result variable, concluding the component successfully.
9. **Error Recording:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final results stored in the result variable.
