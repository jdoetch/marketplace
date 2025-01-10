The **CrowdStrike Falcon - Get Host Vulnerabilities by Incident** component automates the retrieval of vulnerability details for hosts linked to specific incidents within CrowdStrike Falcon. The workflow begins by initializing necessary variables and validating the provided incident ID. It then extracts the host ID from the incident ID, queries CrowdStrike Falcon for detections related to that host, and retrieves summaries of these detections. The component consolidates the detection summaries and updates the final result variable. Throughout the process, comprehensive error handling mechanisms are in place to capture and record any issues, maintaining the integrity and reliability of vulnerability management operations.

## Actions and Their Purpose

### Create Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations. These include:
- Incident_id: The identifier of the incident for which host vulnerabilities are to be retrieved.
- ActionError: Tracks any errors that occur during execution.
- result: Stores the final output results.

**On Success:** Proceeds to Conditional_Parallel.

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
  - **Expression:** [
      {
          "Host Vulnerabilities": actions.Spotlight_Search_for_Vulnerabilites_by_host_id.result,
          "Host Vulnerabilities Error": actions.Spotlight_Search_for_Vulnerabilites_by_host_id.error
      }
  ]
  - **Data:** References the detection summaries and any errors.

### Update_Results
**Type:** updateVariables  
**Purpose:** Updates the result variable with the consolidated detection summaries from Get_Results.

**On Success:** The component’s execution concludes successfully.

**Inputs:**
- result:
  - **Operation:** set
  - **Value:** actions.Get_Results.result

### Action_Error_Update
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable to indicate the successful completion of actions.

**Inputs:**
- Action_Error:
  - **Operation:** set
  - **Value:** Action Completed

### Spotlight_Search_for_Vulnerabilites_by_host_id
**Type:** http  
**Purpose:** Searches for vulnerabilities associated with a specific host ID using CrowdStrike Falcon's Spotlight API.

**On Success:** Calls Action_Error_Update.  
**On Failure:** Calls Action_Error.

**Inputs:**
- endpoint: https://api.crowdstrike.com/spotlight/combined/vulnerabilities/v1
- method: GET
- headers: 
  - Content-Type: application/json (if applicable)
- queryParameters: 
  - filter: aid:'{ $:ref: $actions.Split_Host_Id_from_Incident_Id.result.get_host_id_from_inc }'
  - status: open
  - limit: 400
  - cve.exploit_status:['90']
  - cve.exprt_rating:['CRITICAL']
- settings: 
  - followRedirects: true
  - verifyCertificates: true
  - allowUnsafeLegacyRenegotiation: false

### Split_Host_Id_from_Incident_Id
**Type:** transformation  
**Purpose:** Extracts the host ID from the provided incident ID.

**On Success:** Calls Spotlight_Search_for_Vulnerabilites_by_host_id.

**Transformations:**
- **get_host_id_from_inc:**
  - **Expression:** $split(variables.Incident_id, ":")[1]
  - **Data:** References the Incident_id variable.

### Component_Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations.

**Inputs:**
- Incident_id: References the input Incident_Id.
- ActionError: {}
- result: {}

**On Success:** Proceeds to Conditional_Parallel.

## Process Flow Summary

1. **Initialization:** The component begins by initializing necessary variables, including the incident ID and error tracking.
2. **Input Validation:** Validates the provided Incident_id to ensure it meets the expected conditions.
   - If invalid, it raises and records an error.
   - If valid, it proceeds to extract the host ID from the incident ID.
3. **Host ID Extraction:** Extracts the host ID from the provided incident ID.
4. **Vulnerability Search:** Executes a vulnerability search using CrowdStrike Falcon's Spotlight API based on the extracted host ID.
   - If the search fails, it raises and records an error.
   - If successful, it retrieves and processes detection summaries.
5. **Result Consolidation:** Consolidates the detection summaries into the result variable.
6. **Finalization:** Updates the result variable, concluding the component successfully.
7. **Error Recording:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final results stored in the result variable.