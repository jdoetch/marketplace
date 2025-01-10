# MxToolbox - Check DNS Info: Technical Documentation

## Overview
The "MxToolbox - Check DNS Info" component is an essential automation solution designed to perform DNS lookups and gather DNS information effectively, playing a crucial role in network management and security assessments.

## Component Summary
This component integrates various actions to manage DNS information, each tailored to specific aspects of DNS data handling and analysis. The straightforward process incorporates actions like variable creation, data enrichment transformations, and DNS information retrieval through API calls, followed by error handling and data normalization.

### Actions Description
#### `Create_Variables`
- **Type:** Create Variables
- **Purpose:** Initializes necessary variables for the process.
- **On-Success:** Triggers the `Toolbox_Get_DNS_Info` action.
- **Inputs:** Includes `enrichment` variables setup.

#### `Toolbox_Get_DNS_Info`
- **Type:** HTTP
- **Purpose:** Fetches DNS information from MxToolbox API.
- **On-Success:** Triggers `Create_Enrichment`.
- **On-Failure:** Triggers `Normalize_CreateError_ATWC`.
- **Inputs:** Utilizes endpoint setups and methods to interact with the MxToolbox API services.

#### `Create_Enrichment`
- **Type:** Transformation
- **Purpose:** Transforms the fetched DNS data into structured formats for further analysis.
- **On-Success:** Initiates `Update_Enrichment`.
- **Inputs and Transformations:** Operates transformations on the DNS data to extract core elements and reformat them appropriately.

#### `Update_Enrichment`
- **Type:** Update Variables
- **Purpose:** Updates enriched data variables with newly transformed data.
- **Inputs:** Directly uses results from `Create_Enrichment` as input.

#### `Normalize_CreateError_ATWC`
- **Type:** Connector
- **Purpose:** Handles potential errors in DNS information retrieval, normalizing error data.
- **On-Failure:** Attempt normal operations or log errors for troubleshooting.
- **Inputs:** Error specifics from `Toolbox_Get_DNS_Info`.

### Process Flow
1. Initialize necessary variables.
2. Retrieve DNS data from the API.
3. Transform and enrich DNS information.
4. Update system with newly structured data.
5. Normalize and manage any errors during the process.

### Overall Process Flow Summary
The component follows a structured path from initialization of variables, through data retrieval and transformation, to updating and error handling. This ensures that the DNS information is not only fetched but also appropriately processed and integrated into the system, fostering enhanced operational efficiency and insight into DNS configurations and issues.

