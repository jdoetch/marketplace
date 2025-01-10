This Anomali Threatstream component takes a TEDS observable, queries it against Anomali, and returns a TEDS reputation enrichment. The observable is searched against Anomali, returning only active reports that have a high confidence score. The resulting reports are then used to provide a reputation enrichment of the observable based on the Anomali Threat Score. This component integrates with Swimlane's Turbine Extendable Data Schema, used in the Swimlane Turbine SOC Solution. This common data model allows security practitioners to standardize data across many security tools for common security events, enrichments, and remediations in Swimlane's Turbine platform.


Usage:

- Install the component
- Configure the Anomali Threatstream asset with the URL, API Key, and API User
- Add and configure the component in the desired playbook or component
  - Optional: If configuring this with the Swimlane Turbine SOC Solution, add the Anomali component to the Enrich - Enrich Observable component
  - Add the Enrich - Anomali Threatstream (VIC) component
  - Configure the observable_type and observable_value inputs on the action
