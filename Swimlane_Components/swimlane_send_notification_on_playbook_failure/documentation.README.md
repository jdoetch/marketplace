This Swimlane playbook leverages Personal Access Tokens (PATs) as credentials to identify and retrieve failed playbook runs along with their associated jobs. It consolidates the errors into a summarized message that provides actionable insights for troubleshooting.

The playbook includes customizable actions for error message formatting, enabling teams to tailor notifications to their specific needs. By default, it integrates with the Microsoft Graph API to send email notifications, ensuring prompt communication of playbook failures. Additionally, its flexible design allows seamless integration with alternative platforms such as Gmail, Slack, or Microsoft Teams, making it adaptable to diverse operational environments.

**Usage:**
- Import the playbook
- Configure the following assets:
  - Turbine_Admin__Personal_Access_Token_PAT - (PAT Token of an Admin)
  - Graph_API_Credentials
  - Tenant_Details - All these are present in the URL
    - URL 
    - account_id 
    - tenant_id
- Update the "Send Email" action with appropriate sender details