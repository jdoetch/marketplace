This component streamlines email ingestion from the Graph API by processing emails and extracting all attachments, then converting the data into TEDS format. It includes an option to mark emails as read when the appropriate parameter is provided. Designed for seamless plug-and-play integration with SOC Solution, it enhances efficiency and adaptability within your workflows.



Usage:

- Install the component

- Configure the "Graph API Asset" Asset with Scope, Client ID, Client Secret, and an updated token URL

- Create a playbook for ingestion or utilize an existing playbook

- Add the new "Graph API - Ingest Email with Attachments" component

- Configure the account_email, mark_as_read and filter_query component inputs