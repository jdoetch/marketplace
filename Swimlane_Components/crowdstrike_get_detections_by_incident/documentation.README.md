# CrowdStrike Falcon - Get Detections by Incident

### Summary

The **CrowdStrike Falcon - Get Detections by Incident** component automates the retrieval of detections linked to particular incidents within CrowdStrike Falcon. The workflow initiates by creating necessary variables and validating the provided incident ID. It then queries CrowdStrike Falcon to obtain detections related to the specified incident, processes the detection summaries, and compiles the results into a structured format. The component concludes by updating the result variable with the consolidated data. Throughout the process, comprehensive error handling mechanisms are in place to capture and record any issues, maintaining the integrity and reliability of detection management operations.

## Actions and Their Purpose

### Create Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations. These include:
- Incident_id: The identifier of the incident for which detections are to be retrieved.
- ActionError: Tracks any errors that occur during execution.
- result: Stores the final output results.

**On Success:** Proceeds to Optional_Transform_incoming_data.

### Optional_Transform_incoming_data
**Type:** transformation  
**Purpose:** Prepares and transforms incoming data for downstream actions.

**On Success:** Calls Conditional_Parallel.

**Transformations:**
- **optional_transform:**
  - **Expression:** $eval('"Incoming Transform Data"')

### Conditional_Parallel
**Type:** parallelGroup  
**Purpose:** Manages multiple conditional checks and subsequent actions simultaneously. It ensures that the incident ID is valid before proceeding with the detection retrieval process.

**On Success:** Calls Get_Results.

#### Within Conditional_Parallel:

##### Input Validation
**Type:** conditional  
**Purpose:** Validates that the provided Incident_id meets the expected conditions required by downstream actions.

**Conditions:** 
- Checks if Incident_id is not equal to null.

**Else:** Calls Input_Validation_Error.

##### Input_Validation_Error
**Type:** python  
**Purpose:** Executes a script to raise a custom error message when input validation fails.

**On Success:** Calls updateVariables_a9aj2.

**Inputs:**
- errorRaised: true

##### updateVariables_a9aj2
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable with details from the Input_Validation_Error action.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** actions.Input_Validation_Error.result

##### Action_Error_Update
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable to indicate the successful completion of actions.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** Action Completed

##### Action_Error
**Type:** python  
**Purpose:** Executes a script to raise an error if the Query_Detections_by_Incident_ID action fails.

**On Success:** Calls Update_Action_Error.

**Inputs:**
- errorRaised: true

##### Update_Action_Error
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable with details from the Action_Error action.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** actions.Action_Error.result

##### Query_Detections_by_Incident_ID
**Type:** connector  
**Purpose:** Queries CrowdStrike Falcon to retrieve detections associated with the specified incident ID.

**On Success:** Calls Get_Detection_Summaries.  
**On Failure:** Calls Action_Error.

**Inputs:**
- parameters:
  - q: References the Incident_id variable.
- verify_ssl: true

##### Get_Detection_Summaries
**Type:** connector  
**Purpose:** Retrieves summaries of the detections obtained from the Query_Detections_by_Incident_ID action.

**On Success:** Calls Action_Error_Update.  
**On Failure:** No specific failure actions.

**Inputs:**
- json_body:
  - ids: References the resources from the Query_Detections_by_Incident_ID action result.
- verify_ssl: true

### Get_Results
**Type:** transformation  
**Purpose:** Consolidates the detection summaries into a final result object.

**On Success:** Calls Update_Results.

**Transformations:**
- **results:**
  - **Expression:** actions.Get_Detection_Summaries.result.body.resources
  - **Data:** References the detection summaries.

### Update_Results
**Type:** updateVariables  
**Purpose:** Updates the result variable with the consolidated detection summaries from Get_Results.

**On Success:** The component’s execution concludes successfully.

**Inputs:**
- result:
  - **Operation:** set
  - **Value:** actions.Get_Results.result.results

### Action_Error_Update
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable to indicate the successful completion of actions.

**Inputs:**
- Action_Error:
  - **Operation:** set
  - **Value:** Action Completed

### Component_Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations.

**Inputs:**
- Incident_id: References the input Incident_Id.
- ActionError: {}
- result: {}

**On Success:** Proceeds to Optional_Transform_incoming_data.

## Process Flow Summary

1. **Initialization:** The component begins by initializing necessary variables, including the incident ID and error tracking.
2. **Input Validation Prep:** It prepares and transforms incoming data required for the vulnerability search.
3. **Input Validation:** Validates the provided Incident_id to ensure it meets the expected conditions.
   - If invalid, it raises and records an error.
   - If valid, it proceeds to query detections by the specified incident ID.
4. **Detection Query:** Queries CrowdStrike Falcon to retrieve detections associated with the provided incident ID.
   - If the query fails, it raises and records an error.
   - If successful, it retrieves and processes detection summaries.
5. **Result Consolidation:** Consolidates the detection summaries into the result variable.
6. **Finalization:** Updates the result variable, concluding the component successfully.
7. **Error Recording:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final results stored in the result variable.