This component ingests alerts from Devo, supporting multi-tenancy for flexible deployment. It is compatible with CIM and SOC Solution, enabling seamless integration and efficient alert management within your workflows.

Usage:

- Install the component
- Configure the "Devo Ingest Credentials" Asset with URL and Token
- Create a playbook for ingestion or utilize an existing playbook
- Add a Cron trigger
- Add the new "Devo - Alert Ingest" component to the cron trigger flow
- Name and configure the component action
- Set the Ingestion Interval (In Minutes) component input