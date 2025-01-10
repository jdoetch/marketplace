The Jira Field Data Retrieval component automatically extracts field metadata from all issue types within a specified Jira project. This component retrieves detailed schema information for each field, including custom fields, making it invaluable for tailored Jira implementations. If persistent storage of the retrieved data is required, the component supports writing the data to a custom application for efficient storage and management.


The output for each field includes:

- Issue Type

- Field Name

- Field Key

- Field Type

- Required Field

- Field Options (if applicable, such as for dropdown lists)

 

Usage:

- Install the component

- Configure a Jira asset with administrator privileges (Basic Auth works for this component)

- Assign administrator Jira asset to the "Get Project" and "Get Issue Field Metadata" actions

- Create a playbook for ingestion or utilize an existing playbook

- Configure Jira URL and Project Key component inputs

- Optional: Create a custom application with the proper corresponding fields and output the component response to the application to view the data in a Turbine Application