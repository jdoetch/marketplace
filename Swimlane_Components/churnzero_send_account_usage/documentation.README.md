The ChurnZero Usage Data component enables streamlined transmission of usage data to a ChurnZero account. By efficiently processing and sending data, this integration ensures accurate and timely updates, enhancing customer engagement and analytics within the ChurnZero platform.

 

Usage:

- Install the component

- Configure the "CZ Application Key" Asset with Key and Value (API key)

- Create a new playbook or use an existing one

- Add the new "CZ - Send Account Usage (VIC)" component to the playbook

- Name and configure the component action

- Configure the component inputs:

  - event_name = Usage event name
  - event date = Usage event date
  - description = Usage event description
  - quantity = Must be a number
  - cz_url = Your ChurnZero URL
  - contact_email = ChurnZero contact to associate the event entry with. If this email doesn’t exist in        ChurnZero, a new contact will be created
  - account_id = ChurnZero account ID to associate the event with. This is generally Salesforce ID. If the ID does not exist, a new account will be created.