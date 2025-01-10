### Summary

The **CrowdStrikeFalcon - Upload File or Script to CS Cloud** component automates the process of uploading files or scripts to the CrowdStrike Falcon Cloud. The workflow begins by initializing necessary variables, validating the input attachments, and preparing the file information. It then checks if the file already exists in the CrowdStrike environment to prevent duplicate uploads. If the file does not exist, it proceeds to upload the file or script. After a successful upload, it retrieves the updated file list to confirm the addition. The component consolidates the results and updates the final output variable. Throughout the process, it handles errors to maintain the integrity and reliability of file management operations.

## Actions and Their Purpose

### Create Variables
**Type:** createVariables  
**Purpose:** Initializes essential variables required for the component's operations. These include:
- attachment: References the input attachments.
- result: Stores the final output results.
- Action_Error: Tracks any errors that occur during execution.

**On Success:** Proceeds to Input_Validation_Prep.

### Input_Validation_Prep
**Type:** transformation  
**Purpose:** Prepares and validates the attachment information before proceeding with further actions.

**On Success:** Calls parallel_avj83.

**Transformations:**
- **attachment:**
  - **Expression:** variables.attachment
- **file_name:**
  - **Expression:** actions.Input_Validation_Prep.result.attachment.file_name

### parallel_avj83
**Type:** parallelGroup  
**Purpose:** Manages multiple conditional checks and subsequent actions simultaneously. It ensures that the attachment is valid and determines whether the file already exists before attempting an upload.

**On Success:** Calls Get_Results.

#### Within parallel_avj83:

##### Input_Validation_IF_Condition
**Type:** conditional  
**Purpose:** Validates that the attachment is not null before proceeding with the file upload process.

**Conditions:** 
- Checks if attachment is not equal to null.

**Else:** Calls Input_Validation_ErrorRaise.

##### Input_Validation_ErrorRaise
**Type:** python  
**Purpose:** Executes a script to raise a custom error message when input validation fails.

**On Success:** Calls Update_Action_Error_with_Input_Validation_Error.

**Inputs:**
- errorRaised: true

##### Update_Action_Error_with_Input_Validation_Error
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable with details from the Input_Validation_ErrorRaise action.

##### getRTRPutFiles
**Type:** connector  
**Purpose:** Queries CrowdStrike Falcon to retrieve the list of files currently uploaded, ensuring that duplicate files are not uploaded.

**On Success:** Calls GetFIrstFileLIst.  
**On Failure:** No specific failure actions.

**Inputs:**
- parameters:
  - ids: []
- verify_ssl: true

##### GetFIrstFileLIst
**Type:** transformation  
**Purpose:** Processes the list of existing files to determine if the file to be uploaded already exists.

**On Success:** Calls If_file_exists_in_file_list.

**Transformations:**
- **filelist:**
  - **Expression:** $distinct(actions.getRTRPutFiles.result.body.resources[].name)
- **file_name:**
  - **Expression:** actions.Input_Validation_Prep.result.file_name
- **exists:**
  - **Expression:** $lowercase(actions.GetFIrstFileLIst.result.file_name) in actions.GetFIrstFileLIst.result.filelist

##### If_file_exists_in_file_list
**Type:** conditional  
**Purpose:** Determines the next steps based on whether the file already exists in CrowdStrike Falcon.

**Conditions:** 
- Checks if exists is true.

**Else:** Calls Put_File.

**On Success:**  
- If file exists, calls Prepare_Outputs.

**On Failure:**  
- If file does not exist, proceeds to upload the file.

##### Prepare_Outputs
**Type:** transformation  
**Purpose:** Prepares the output data when the file already exists.

**On Success:** Calls Action_Error_Update_File_already_Exists.

**Transformations:**
- **put:**
  - **Expression:** [{"put_result": actions.Put_File.result, "put_error": actions.Put_File.error}]
- **getfilelist:**
  - **Expression:** actions.getRTRPutFiles_New_File_added.result.body.resources

##### Action_Error_Update_File_already_Exists
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable to indicate that the file already exists and the file list has been refreshed.

**Inputs:**
- Action_Error:
  - **Operation:** set
  - **Value:** File already exists - File list refreshed

##### Put_File
**Type:** http  
**Purpose:** Uploads the specified file or script to CrowdStrike Falcon Cloud.

**On Success:** Calls getRTRPutFiles_New_File_added.  
**On Failure:** No specific failure actions.

**Inputs:**
- endpoint: https://api.crowdstrike.com/real-time-response/entities/put-files/v1
- method: POST
- headers: 
  - Content-Type: multipart/form-data
- body: 
  - file: References the attachment variable

##### getRTRPutFiles_New_File_added
**Type:** connector  
**Purpose:** Retrieves the updated list of files after a successful upload to confirm the addition.

**On Success:** Calls Prepare_Outputs_with_new_file_added.  
**On Failure:** No specific failure actions.

**Inputs:**
- parameters:
  - ids: []
- verify_ssl: true

##### Prepare_Outputs_with_new_file_added
**Type:** transformation  
**Purpose:** Processes the results of the file upload and prepares the final output data.

**On Success:** Calls Action_Error_Update_with_new_file_added.

**Transformations:**
- **put:**
  - **Expression:** [{"put_result": actions.Put_File.result, "put_error": actions.Put_File.error}]
- **getfilelist:**
  - **Expression:** actions.getRTRPutFiles_New_File_added.result.body.resources

##### Action_Error_Update_with_new_file_added
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable to indicate the successful completion of the file upload.

**Inputs:**
- Action_Error:
  - **Operation:** set
  - **Value:** Action Completed with new file added

##### Action_Error
**Type:** python  
**Purpose:** Executes a script to raise an error if the queryHostByIndicator action fails.

**On Success:** Calls Update_Action_Error.

**Inputs:**
- errorRaised: true

##### Update_Action_Error
**Type:** updateVariables  
**Purpose:** Updates the Action_Error variable with details from the Action_Error action.

### Get_Results
**Type:** transformation  
**Purpose:** Consolidates the results of the file upload and host information retrieval into a final result object.

**On Success:** Calls Update_Results.

**Transformations:**
- **results:**
  - **Expression:** [{"file exists": actions.Prepare_Outputs.result, "put file": actions.Prepare_Outputs_with_new_file_added.result}]

### Update_Results
**Type:** updateVariables  
**Purpose:** Updates the result variable with the consolidated results from Get_Results.

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
- type: ipv4
- value: 8.8.8.8
- ActionError: {}
- result: {}

**On Success:** Proceeds to Conditional_Parallel.

## Process Flow Summary

1. **Initialization:** The component begins by initializing necessary variables, including the indicator type (ipv4), value (8.8.8.8), and error tracking.
2. **Input Validation Prep:** It prepares the attachment information and extracts the file name for validation.
3. **Input Validation:** Validates the provided type and value to ensure they meet the expected conditions.
   - If invalid, it raises and records an error.
   - If valid, it proceeds to query hosts by the specified indicator.
4. **Host Query:** Queries CrowdStrike Falcon to search for hosts based on the provided IPv4 address.
   - If the query fails, it raises and records an error.
   - If successful, it retrieves detailed information about the identified hosts.
5. **File Existence Check:** Checks if the file to be uploaded already exists in CrowdStrike Falcon to prevent duplicates.
   - If the file exists, it records that the file already exists and refreshes the file list.
   - If the file does not exist, it proceeds to upload the file.
6. **File Upload:** Uploads the specified file or script to CrowdStrike Falcon Cloud.
   - After a successful upload, it retrieves the updated file list to confirm the addition.
7. **Result Consolidation:** Consolidates the results of the file upload and host information retrieval into the result variable.
8. **Finalization:** Updates the result variable, concluding the component successfully.
9. **Error Recording:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.