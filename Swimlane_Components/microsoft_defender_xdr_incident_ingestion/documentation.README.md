The Defender XDR Incident Ingestion component automatically ingests Microsoft Defender XDR Incidents into your Turbine platform. This component retrieves Defender XDR Incidents and their associated alerts, extracts indicators of compromise, and transforms the data into the Swimlane Turbine Extendable Data Schema for use in conjunction with other playbooks like Swimlane's SOC Solution.

Usage:

- Install the component
- Configure the "Microsoft Defender" Asset with Client ID, Client Secret, and an updated Token URL
- Create a playbook for ingestion or utilize an existing playbook
- Add a Cron trigger
- Add the new "Ingest - Microsoft XDR Incident (VIC)" component to the cron trigger flow
- Name and configure the component action
    - Set the limit, the number of incidents to retrieve (max 100)
    - Set the timeframe, the window of incidents to ingestion, in the format "<time window: number> <time scale: seconds, minutes, hours> ago", e.g., "20 minutes ago"
    - Set the statuses, a comma-separated list of statuses to filter the Incidents by, e.g., "Active" or "Active,Resolved"
- Optional: To process via SOC Solution, add a new component action after the ingest action, "Execute - Process Bulk Alerts" and map the result of the ingestion component to the input of the Process Bulk Alerts component