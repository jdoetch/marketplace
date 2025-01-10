# CrowdStrike Falcon Spotlight - Search with Keyword and Return Hosts with Matching Vulnerabilities

## Short Description

This component enables security analysts to search for vulnerabilities across endpoints managed by CrowdStrike Falcon using specific keywords. It streamlines the process of identifying hosts with matching vulnerabilities by validating input parameters, executing search queries, and compiling the results. Comprehensive error handling ensures reliable and efficient vulnerability management within the CrowdStrike Falcon environment.

## Summary

The **CrowdStrike Falcon Spotlight - Search with Keyword and Return Hosts with Matching Vulnerabilities** component automates the process of searching for vulnerabilities across endpoints based on user-defined keywords. The workflow initiates by creating necessary variables and validating the input parameters to ensure they meet the expected criteria. It then executes a vulnerability keyword search using CrowdStrike Falcon's API, processes the search results, and compiles the relevant host information with matching vulnerabilities. The component finalizes by updating the result variable with the consolidated data. Throughout the process, robust error handling mechanisms are in place to capture and record any issues, maintaining the integrity and reliability of the vulnerability management operations.

## Actions and Their Purpose

### Create Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations. These include:
- keyword: The keyword used to search for vulnerabilities.
- filter: Additional filters to refine the search results.
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
**Purpose:** Manages multiple conditional checks and subsequent actions simultaneously. It ensures that the input parameters are valid before proceeding with the vulnerability search process.

**On Success:** Calls Get_Results.

#### Within Conditional_Parallel:

##### Input Validation
**Type:** conditional  
**Purpose:** Validates that the necessary input parameters meet the expected conditions required by downstream actions.

**Conditions:** 
- Checks if the placeholder variables needed by actions are not equal to null.

**Else:** Calls Input_Validation_Error.

##### Input_Validation_Error
**Type:** python  
**Purpose:** Executes a script to raise a custom error message when input validation fails.

**On Success:** No subsequent actions.

**Inputs:**
- errorRaised: true

##### Action_Error_Update
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable to indicate the successful completion of actions.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** $:ref: $eval("Action Completed")

##### Action_Error
**Type:** python  
**Purpose:** Executes a script to raise an error if the getResultsFromVulnerabilityKeywordSearch_aoh67 action fails.

**On Success:** Calls Update_Action_Error.

**Inputs:**
- errorRaised: true

##### Update_Action_Error
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable with details from the Action_Error action.

##### getResultsFromVulnerabilityKeywordSearch_aoh67
**Type:** connector  
**Purpose:** Executes a vulnerability keyword search using CrowdStrike Falcon's API based on the provided keyword and filter.

**On Success:** Calls Action_Transform.  
**On Failure:** Calls Action_Error.

**Inputs:**
- json_body:
  - keyword: References the keyword variable.
  - filter: References the filter variable.
- verify_ssl: true

##### Action_Transform
**Type:** transformation  
**Purpose:** Processes the results obtained from the vulnerability keyword search.

**On Success:** Calls Action_Error_Update.  
**On Failure:** No subsequent actions.

**Transformations:**
- **result:**
  - **Expression:** actions.getResultsFromVulnerabilityKeywordSearch_aoh67.result.json_body
  - **Data:** References the search results.

### Get_Results
**Type:** transformation  
**Purpose:** Consolidates the results from the vulnerability search into a final result object.

**On Success:** Calls Update_Results.

**Transformations:**
- **results:**
  - **Expression:** $lookup(actions.Action_Transform.result,'result')
  - **Data:** References the transformed search results.

### Update_Results
**Type:** updateVariables  
**Purpose:** Updates the result variable with the consolidated results from Get_Results.

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

### Input_Validation_Update_Error
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable with details from the Input_Validation_ErrorRaise action.

**Inputs:**
- Action_Error:
  - **Operation:** set
  - **Value:** actions.Input_Validation_ErrorRaise.result

### queryHostByIndicator
**Type:** connector  
**Purpose:** Queries CrowdStrike Falcon to search for hosts based on the provided indicator type and value.

**On Success:** Calls getHostInfo.  
**On Failure:** Calls Action_Error.

**Inputs:**
- parameters:
  - type: References the type variable.
  - value: References the value variable.
- verify_ssl: true

### getHostInfo
**Type:** connector  
**Purpose:** Retrieves detailed information about the hosts identified by the queryHostByIndicator action.

**On Success:** Calls Action_Error_Update.  
**On Failure:** No specific failure actions.

**Inputs:**
- parameters:
  - ids: References the resources from the queryHostByIndicator action result.
- verify_ssl: true

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
- keyword: References the input keyword.
- filter: References the input filter.
- ActionError: {}
- result: {}

**On Success:** Proceeds to Optional_Transform_incoming_data.

## Process Flow Summary

1. **Initialization:** The component begins by initializing necessary variables, including the search keyword, filter criteria, and error tracking.
2. **Input Validation Prep:** It prepares and validates the attachment information required for the vulnerability search.
3. **Input Validation:** Validates the provided keyword and filter to ensure they meet the expected conditions.
   - If invalid, it raises and records an error.
   - If valid, it proceeds to execute the vulnerability keyword search.
4. **Vulnerability Search:** Executes a vulnerability keyword search using CrowdStrike Falcon's API based on the provided keyword and filter.
   - If the search fails, it raises and records an error.
   - If successful, it processes the search results.
5. **Result Consolidation:** Consolidates the search results into the result variable.
6. **Finalization:** Updates the result variable, concluding the component successfully.
7. **Error Recording:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final results stored in the result variable.