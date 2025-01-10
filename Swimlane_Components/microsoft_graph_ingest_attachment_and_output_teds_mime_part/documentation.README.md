This Swimlane component facilitates the retrieval of email attachments using the Microsoft Graph API and transforms the data into a TEDS-compliant MIME parts schema. Designed for seamless integration into workflows, it ensures that attachments are efficiently processed and standardized for further analysis and action.

**Usage:**
- Configure Graph API asset
- Retrieve an email ID
- Pass the account email and the email id to the component
- Outputs an array of attachments converted into TEDS Mime Parts

Inputs: 
- account_email - string
- email_id - string

Outputs:
- MIME_Parts - array