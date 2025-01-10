The **CrowdStrikeFalcon - Threat Hunt - Search Endpoints by IOC IPv4 Address** component automates the process of searching for endpoints within CrowdStrike Falcon based on provided IOC IPv4 addresses. The workflow begins by initializing necessary variables, validating the input parameters, and querying hosts using the specified IPv4 indicators. If the inputs are valid and the query is successful, it retrieves detailed information about the identified hosts. The component then consolidates the results and updates the final output variable. Throughout the process, it handles errors to maintain the integrity and reliability of threat hunting operations.

## Actions and Their Purpose

### Create Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations. These include:
- type: Specifies the type of indicator (ipv4).
- value: The IPv4 address used to search for endpoints.
- ActionError: Tracks any errors that occur during execution.
- result: Stores the final output results.

**On Success:** Proceeds to Conditional_Parallel.

### Conditional_Parallel
**Type:** parallelGroup  
**Purpose:** Manages multiple conditional checks and subsequent actions simultaneously. It ensures that input parameters are valid before proceeding with the threat hunting process.

**On Success:** Calls Get_Results.

#### Within Conditional_Parallel:

##### Input_Validation
**Type:** conditional  
**Purpose:** Validates that the provided type and value meet the expected conditions required by downstream actions.

**Conditions:** 
- Checks if type is not equal to null.
- Checks if value is not equal to null.

**Else:** Calls Input_Validation_Error.

##### Input_Validation_Error
**Type:** python  
**Purpose:** Executes a script to raise a custom error message when input validation fails.

**On Success:** Calls Input_Validation_Update_Error.

**Inputs:**
- errorRaised: true

##### Input_Validation_Update_Error
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable with details from the Input_Validation_Error action.

##### queryHostByIndicator
**Type:** connector  
**Purpose:** Queries CrowdStrike Falcon to search for hosts based on the provided indicator type and IPv4 address.

**On Success:** Calls getHostInfo.  
**On Failure:** Calls Action_Error.

**Inputs:**
- parameters:
  - type: References the type variable.
  - value: References the value variable.
- verify_ssl: true

##### Action_Error
**Type:** python  
**Purpose:** Executes a script to raise an error if the queryHostByIndicator action fails.

**On Success:** Calls Update_Action_Error.

**Inputs:**
- errorRaised: true

##### Update_Action_Error
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable with details from the Action_Error action.

##### getHostInfo
**Type:** connector  
**Purpose:** Retrieves detailed information about the hosts identified by the queryHostByIndicator action.

**On Success:** Calls Action_Error_Update.  
**On Failure:** No specific failure actions.

**Inputs:**
- parameters:
  - ids: References the resources from the queryHostByIndicator action result.
- verify_ssl: true

##### Action_Error_Update
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable to indicate the successful completion of actions.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** $:ref: $eval("Action Completed")

### Get_Results
**Type:** transformation  
**Purpose:** Consolidates the host information retrieved by getHostInfo into a final result object.

**On Success:** Calls Update_Result_Variable.

**Transformations:**
- **results:**
  - **Expression:** actions.getHostInfo.result

### Update_Result_Variable
**Type:** updateVariables  
**Purpose:** Updates the result variable with the consolidated results from Get_Results.

**On Success:** The component’s execution concludes successfully.

**Inputs:**
- result:
  - **Operation:** set
  - **Value:** $:ref: $actions.Get_Results.result

### RaiseError
**Type:** python  
**Purpose:** Executes a script to raise an error if any action fails after input validation.

**On Success:** Calls Update_Action_Error.

**Inputs:**
- errorRaised: true

### Update_Action_Error
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable with details from the error raised by RaiseError.

### Action_Error_Update
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable to indicate the successful completion of actions.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** $:ref: $eval("Action Completed")

### Input_Validation_Update_Error
**Type:** updateVariables  
**Purpose:** Updates the ActionError variable with details from the Input_Validation_Error action.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** $:ref: $actions.Input_Validation_Error.result

### queryHostByIndicator
**Type:** connector  
**Purpose:** Queries CrowdStrike Falcon to search for hosts based on the provided indicator type and IPv4 address.

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
**Purpose:** Updates the ActionError variable to indicate the successful completion of actions.

**Inputs:**
- ActionError:
  - **Operation:** set
  - **Value:** $:ref: $eval("Action Completed")

### Component_Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations.

**Inputs:**
- type: ipv4
- value: 8.8.8.8
- ActionError: {}
- result: {}

**On Success:** Proceeds to Conditional_Parallel.

## Process Flow Summary

1. **Initialization:** The component begins by initializing necessary variables, including indicator type (ipv4), value (8.8.8.8), and error tracking.
2. **Input Validation:** It validates the provided type and value to ensure they meet the expected conditions.
   - If invalid, it raises and records an error.
   - If valid, it proceeds to query hosts by the specified indicator.
3. **Host Query:** Queries CrowdStrike Falcon to search for hosts based on the provided indicator type and IPv4 address.
   - If the query fails, it raises and records an error.
   - If successful, it retrieves detailed information about the identified hosts.
4. **Result Consolidation:** Consolidates the retrieved host information into the result variable.
5. **Finalization:** Updates the result variable, concluding the component successfully.
6. **Error Recording:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final results stored in the result variable.