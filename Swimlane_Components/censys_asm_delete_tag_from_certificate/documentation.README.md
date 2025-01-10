# Censys ASM - Delete Tag from a Certificate

## Overview
The "Censys ASM - Delete Tag from a Certificate" component is designed to automate the management of security certificates by facilitating the deletion of tags associated with them. This document details each action within the component's flow, explaining its purpose, operational type, subsequent steps, and overall integration flow in a sequence that ensures clarity and comprehension for end users.

### Short Description
The component exists to enhance security management practices by allowing users to efficiently delete unnecessary or outdated tags from certificates, ensuring that certificate metadata remains relevant and up to date.

### Summary of the Component
This component coordinates several actions involving variables, transformations, and HTTP requests to interact with the Censys API, updating records as required. It is structured to handle potential errors gracefully, ensuring that system integrity is maintained even during failure scenarios.

### Actions Description
1. **Create Variables**
   - **Type:** Variable Creation
   - **Purpose:** Initializes variables for use later in the component's workflow.
   - **On-success:** Proceeds to send an HTTP _equest.
   - **On-failure:** None specified.

2. **Update Enrichment**
   - **Type:** Update Variables
   - **Purpose:** Updates the values of variables based on results from the Create nrichment action.
   - **On-success:** None specified.
   - **On-failure:** None specified.

3. **Create Enrichment**
   - **Type:** Transformation
   - **Purpose:** Transforms data received from actions to annotate or modify the enrichment data for a certificate.
   - **On-success:** Triggers the Update Enrichment action.
   - **On-failure:** None specified.

4. **Normalize and React to Error (normalize_reaterror_atwc)**
   - **Type:** Connector
   - **Purpose:** Normalizes error output and formats it correctly for logging or further error handling.
   - **On-success:** Updates enrichment with normalized data.
   - **On-failure:** None specified.

5. **_equest**
   - **Type:** HTTP Request
   - **Purpose:** Makes a direct HTTP request to the Censys API to delete a tag from a certificate.
   - **On-success:** If successful, proceeds to Create Enrichment.
   - **On-failure:** Executes the Normalize and React to Error action.

### Overall Process Flow Summary
The component starts by creating necessary variables, followed by an HTTP request to delete a specified tag. On successful deletion, it transforms and updates the enrichment data. If the HTTP request fails, it normalizes the error and updates the enrichment based on error data. This structured flow ensures robust handling of the delete operation from initiation to completion, including error management.

