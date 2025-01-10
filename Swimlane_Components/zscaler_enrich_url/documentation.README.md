This ZScaler Enrich URL component takes a TEDS observable(URL), submits it to ZScaler URL Lookup endpoint, and returns a TEDS reputation enrichment. This component integrates with Swimlane's Turbine Extendable Data Schema. This common data model allows security practitioners to standardize data across many security tools for common security events, enrichments and remediations in Swimlane's Turbine platform.

**Inputs:**
* observable_url - string

**Outputs:**
* TEDS Enrichment Object

**Usage:**
* Configure ZScaler asset
* Drop component into a playbook
* Pass a URL to the component
* It will return an enrichment object

