# Playbook Documentation: Azure - Revoke Signin Sessions

## Summary
The Azure - Revoke Signin Sessions is designed to manage user account sessions in an automated workflow. Specifically, it revokes user sign-in sessions using the Microsoft Graph API and records the outcomes of each action for process monitoring and troubleshooting.

### Key Features:
- **Automated Session Revocation**: Uses Microsoft Graph API to revoke a user's active sessions.
- **Dynamic Response Handling**: Updates playbook variables with the result of the session revocation process.
- **Error Management**: Provides detailed feedback for both success and failure scenarios.

---

## Entrypoints
The playbook starts execution at the Action_Response step.

---

## Actions Overview

### **1. Action Response**
- **Type**: createVariables
- **Purpose**: Initializes variables for subsequent actions. Specifically, it sets the variable revoke_session_response to Pending.
- **Next Steps**:
  - On success: Proceeds to the Revoke_Signin_Session action.
  - On failure: No additional steps are configured.

#### Inputs:
- **name**: revoke_session_response
- **value**: Pending

---

### **2. Revoke Signin Session**
- **Type**: connector
- **Purpose**: Calls the Microsoft Graph API to revoke the active sign-in sessions for a specified user account.
- **Next Steps**:
  - **On Success**: Proceeds to Success_Revoke_Session.
  - **On Failure**: Proceeds to Failed_to_Revoke_Session.

#### Inputs:
- **path_parameters**: 
  - Contains the user account ID, dynamically referenced as {$inputs.user_account}.
- **verify_ssl**: Ensures SSL verification is enabled.

#### Additional Metadata:
- **Connector Action**: microsoft_graph_api.revoke_signin_sessions
- **Timeout**: 0 (no timeout specified).
- **Pool**: $default

---

### **3. Success Revoke Session**
- **Type**: updateVariables
- **Purpose**: Updates the revoke_session_response variable to indicate the session revocation was successful.
- **Next Steps**:
  - No further actions are configured.

#### Inputs:
- **name**: revoke_session_response
- **operation**:
  - **Type**: set
  - **Value**: Successfully revoked sessions for { $:ref: $inputs.user_account }.

---

### **4. Failed to Revoke Session**
- **Type**: updateVariables
- **Purpose**: Updates the revoke_session_response variable to indicate that the session revocation failed.
- **Next Steps**:
  - No further actions are configured.

#### Inputs:
- **name**: revoke_session_response
- **operation**:
  - **Type**: set
  - **Value**: Failed to revoke sessions for { $:ref: $inputs.user_account }. Refer to failed playbook for details.

---

## Process Flow Summary
1. **Initialization**:
   - The playbook begins at the Action_Response step, initializing the revoke_session_response variable to Pending.

2. **Session Revocation**:
   - The Revoke_Signin_Session action calls the Microsoft Graph API to revoke the specified user's active sessions.
   - Depending on the outcome:
     - **Success**: Updates the revoke_session_response to indicate success and includes the user account ID.
     - **Failure**: Updates the revoke_session_response with an error message and directs users to consult the failed playbook for further details.

3. **Result Publishing**:
   - The playbook concludes by publishing the final response_message variable for external consumption. This variable reflects the result of the revocation process.

---

## Inputs and Requirements

### Inputs
| **Input Name**  | **Description**                                                      | **Type**   | **Required** |
|------------------|----------------------------------------------------------------------|------------|--------------|
| user_account   | The user account to be disabled or enabled depending on the action. | string   | Yes          |
| action         | Specifies the action to perform: enable or disable.             | string   | Yes          |

### Required Permissions
This playbook requires permissions to access the Microsoft Graph API for session revocation.

---

## Triggers
No external triggers are defined for this playbook.

---

## Publishing Details
The playbook publishes the variable response_message, which contains the final state of the revoke_session_response variable.

---

## Additional Notes
- Ensure the user account specified in the inputs is valid and accessible via the Microsoft Graph API.
- The playbook’s success and error messages are dynamically generated to enhance clarity and troubleshooting.