This Nozomi component integrates to Nozomi Guardian via Nozomi's API, the component works with Ingestion playbook's cron schedule, to automatically ingests incoming Nozomi Guardian's Alerts into your Turbine use cases for analysis, enrichment, and response. This component transforms and maps incoming data to Swimlane's Turbine Extendable Data Schema. This common data model allows security practitioners to standardize data across many security tools for common security events, enrichments, and remediations in Swimlane's Turbine platform.

**Instructions**
1. Click "+ Install" to deploy the component into the current Turbine tenant.
2. After component install, setup Nozomi asset.
   - Navigate to the menu, Orchestration > Assets, click the '+' sign at the top right corner, a pop up will be showing "Select An Asset Type"
   - In the "Select An Asset Type" pop up page, keyin 'nozomi' in the 'Search Assets' area on the top right section, select the Nozomi's asset type with HTTP Basic Authentication.
   - Fill up Asset's Title, Name, URL(i.e. https://<ip or fqdn>) of Nozomi Guardian, Username and Password. Click Create, and a new asset shall be created.
3. Update Nozomi Action in the component, with asset defined in (2).
   - Navigate to the menu, Orchestration > Components, go into component named "Nozomi - Guardian - Get Alerts"
   - Click on the Nozomi connection's action named "Query Alerts", an Action panel shall be visible on the right hand side of the screen. Toggle the 'Asset' and select asset defined in (2), and save by clicking the 'Save' button at the top right corner.
4. Integrate into SOC Solutions' playbook, named "Ingest - Alert Ingestion", or replicate a flow "Schedule/Cron" in the playbook if that flow is already being used. 
   - Navigate to the menu, Orchestration > Playbooks, go into the playbook named "Ingest - Alert Ingestion"
   - On the Flow 'Schedule/cron', replace component named "Alert Ingestion VIC" with component named "Nozomi - Guardian - Get Alerts".
   - Edit the Component action, and update inputs organization and start_time.
   - Sample start_time (relative time) accepted by Nozomi: **days_ago(time) < 1** or **hours_ago(time)** < **1 or minutes_ago(time)**
   - Click save to save changes to the playbook.
5. With the above, you are ready to test and run the ingestion.