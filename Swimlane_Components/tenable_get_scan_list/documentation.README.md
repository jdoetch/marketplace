# Tenable.IO - Get Scan List

### Short Description

This component enables security teams to efficiently retrieve and manage vulnerability scan lists from Tenable.io. By automating the launch of scans and extracting detailed scan information, it streamlines the vulnerability management process, ensuring that security analysts have timely and accurate access to scan data for effective decision-making and remediation efforts.

### Summary

The **Tenable.IO - Get Scan List** component automates the process of fetching and processing vulnerability scan lists from Tenable.io. The workflow initiates by launching a specified scan using Tenable.io's API. Upon successful initiation, it retrieves the status of the launched scan, including its UUID, current status, and progress. The component then extracts detailed scan information, filters the scans based on provided criteria such as name and owner, and compiles the results into a structured format. Comprehensive error handling ensures that any issues encountered during the scan launch or data extraction processes are promptly identified and recorded, maintaining the reliability and integrity of vulnerability management operations.

## Actions and Their Purpose

### Tenable Launch Scan
**Type:** connector  
**Purpose:** Initiates a vulnerability scan in Tenable.io using the provided scan ID.

**On Success:** Calls Tenable_Scan_Status.

**Inputs:**
- path_parameters: 
  - scan_id: References the Scan_ID input.

**Action:** tenable_io.launch_scan

### Tenable Scan Status
**Type:** connector  
**Purpose:** Retrieves the current status of a launched vulnerability scan from Tenable.io.

**On Success:** No subsequent actions.

**Inputs:**
- path_parameters: 
  - scan_id: References the Scan_ID input.

**Action:** tenable_io.get_scan_status

### Extract Scans Details
**Type:** transformation  
**Purpose:** Processes and extracts detailed information from the scan list retrieved from Tenable.io.

**On Success:** No subsequent actions.

**Transformations:**
- **scan_results_length:**
  - **Expression:** $count(actions.Tenable_IO_Get_Scan_List.result.json_body.scans)
  - **Purpose:** Counts the total number of scans retrieved.
  
- **filtered_scans:**
  - **Expression:** 
    
    [
      inputs.Name ? actions.Extract_Scans_Details.result.name_scans,
      inputs.Owner ? actions.Extract_Scans_Details.result.owner_scans
    ]
    
  - **Purpose:** Filters scans based on the provided Name and Owner criteria.
  
- **distinct_filtered_scans:**
  - **Expression:** $distinct(actions.Extract_Scans_Details.result.filtered_scans)
  - **Purpose:** Removes duplicate scans from the filtered results.
  
- **filtered_results_length:**
  - **Expression:** $count(actions.Extract_Scans_Details.result.distinct_filtered_scans)
  - **Purpose:** Counts the number of distinct filtered scans.
  
- **scans:**
  - **Expression:** actions.Tenable_IO_Get_Scan_List.result.json_body.scans
  - **Purpose:** Extracts the list of scans from the scan list result.
  
- **name_scans:**
  - **Expression:** $arrayFilterBy(actions.Extract_Scans_Details.result.scans,'name',inputs.Name)
  - **Purpose:** Filters scans by their name.
  
- **owner_scans:**
  - **Expression:** $arrayFilterBy(actions.Extract_Scans_Details.result.scans,'owner',inputs.Owner)
  - **Purpose:** Filters scans by their owner.
  
- **owner_results_length:**
  - **Expression:** $count(actions.Extract_Scans_Details.result.owner_scans)
  - **Purpose:** Counts the number of scans filtered by owner.
  
- **name_results_length:**
  - **Expression:** $count(actions.Extract_Scans_Details.result.name_scans)
  - **Purpose:** Counts the number of scans filtered by name.

### Update Result Variable
**Type:** updateVariables  
**Purpose:** Updates the result variable with the scan UUID, status, and progress obtained from the Tenable.io actions.

**Inputs:**
- scan_uuid: References the Tenable_Launch_Scan.result.json_body.scan_uuid
- status: References the Tenable_Scan_Status.result.json_body.status
- progress: References the Tenable_Scan_Status.result.json_body.progress

**On Success:** The component’s execution concludes successfully.

### Update Issue Variables
**Type:** updateVariables  
**Purpose:** Updates variables with the response from the Jira API after updating the issue.

**Inputs:**
- output_response:
  - **Operation:** set
  - **Value:** actions.Edit_Issue_With_Standard_Fields.result
- output_fields_json:
  - **Operation:** set
  - **Value:** actions.combine_fields.result

### Get Scan List
**Type:** connector  
**Purpose:** Retrieves a list of vulnerability scans from Tenable.io based on specified parameters.

**On Success:** Calls Extract_Scans_Details.

**Inputs:**
- parameters: 
  - last_modification_date: References the Last_Modification_Date input.
  - folder_id: References the Folder_ID input.

**Action:** tenable_io.get_scans_list

### Update Issue
**Type:** connector  
**Purpose:** Updates the Jira issue with the provided fields.

**On Success:** Calls Update_Variables.  
**On Failure:** No specific failure actions.

**Inputs:**
- path_parameters: 
  - issueIdOrKey: References the issue_key input.
- json_body: References the fields input.

**Action:** atlassian_jira.issue_edit

### Combine Fields
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

### Update Variables
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

1. **Initialization:** The component begins by initializing necessary variables, including the scan ID and parameters for retrieving scan lists.
2. **Scan Launch:** It initiates a vulnerability scan in Tenable.io using the provided Scan_ID.
3. **Status Retrieval:** Upon successfully launching the scan, it retrieves the current status and progress of the scan.
4. **Scan Details Extraction:** The component extracts detailed scan information, including counting total scans and filtering based on name and owner criteria.
5. **Result Compilation:** It consolidates the scan UUID, status, progress, and filtered scan details into the result variable.
6. **Finalization:** Updates the result variable, concluding the component successfully.
7. **Error Handling:** At any point of failure, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility.

If any action fails during the process, the component ensures that errors are raised and recorded, preventing further execution and maintaining error visibility. Otherwise, it completes successfully with the final scan details stored in the result variable.