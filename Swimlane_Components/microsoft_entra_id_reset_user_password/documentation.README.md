# Playbook Documentation: Azure - Reset User Password

## Summary
The cAzure - Reset User Password is an automated workflow designed to enforce a password reset for user accounts on their next login. It leverages the Microsoft Graph API to update user attributes and dynamically manages success and failure states through structured variables.

### Key Features:
- **Dynamic Payload Transformation**: Constructs JSON payloads for Microsoft Graph API requests.
- **Automated API Call Handling**: Updates user account settings for password resets.
- **Result Management**: Tracks outcomes and provides actionable status messages.

---

## Entrypoints
The playbook begins at the Action_Response step.

---

## Actions Overview

### **1. Action Response**
- **Type**: createVariables
- **Purpose**: Initializes variables to track the password reset process. Specifically, it sets the variable reset_password_response to Pending.
- **Next Steps**:
  - On success: Proceeds to the JSON_Payload action.
  - On failure: No further actions are configured.

#### Inputs:
- **name**: reset_password_response
- **value**: Pending

---

### **2. JSON Payload**
- **Type**: transformation
- **Purpose**: Constructs a JSON payload required for the Microsoft Graph API request. This payload forces a password change on the user's next login.
- **Next Steps**:
  - On success: Proceeds to Force_Change_Password_Next_Sign_In.
  - On failure: No additional steps are defined.

#### Transformations:
- Constructs the following JSON payload:
  json
  {
    "passwordProfile": {
      "forceChangePasswordNextSignIn": true
    }
  }
