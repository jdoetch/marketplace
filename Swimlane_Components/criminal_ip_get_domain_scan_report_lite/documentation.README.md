# Criminal IP - Get Domain Scan Report Lite

## Overview
The "Criminal IP - Get Domain Scan Report Lite" component is designed for users who need to automate the process of obtaining a domain scan report from Criminal IP. This component helps in evaluating domain reputations by fetching detailed insights based on various parameters. 

## Purpose
The primary purpose of this component is to assess domain security threats and provide an automated response through enriched data. Automation reduces the time and effort required in handling domains analysis and increases the efficiency of security operations.

## Detailed Process Flow

### Create Variables
- **Action Type:** createariables
- **Purpose:** Initializes the variables used for storing results and sends a request.
- **On-Success:** Proceeds to send a request.
- **On-Failure:** Logs or handles error based on system configuration.
  
### Send Request
- **Action Type:** http
- **Purpose:** Sends an HTTP request to Criminal IP for initiating a domain scan.
- **On-Success:** Processes the scan by triggering the transformation action to Create Enrichment.
- **On-Failure:** Handles errors by normalizing and logging the potential errors.

### Create Enrichment
- **Action Type:** transformation
- **Purpose:** Transforms the HTTP request response into a structured format that can be easily updated or enriched further.
- **On-Success:** Updates the enrichment data.
- **On-Failure:** Manages errors by logging and normalization.

### Update Enrichment
- **Action Type:** updateariables
- **Purpose:** Updates the enrichment data based on the transformation results.
- **On-Success:** Completes the process or initiates additional steps as configured.
- **On-Failure:** Initiates error handling routines.

### Normalize Error
- **Action Type:** connector
- **Purpose:** Normalizes any encountered errors during the component execution.
- **On-Success:** Updates enrichment post-error correction.
- **On-Failure:** Logs error and exits.

### Process Flow Summary
The component "Criminal IP - Get Domain Scan Report Lite" starts with initializing variables necessary for the operation. A network request is made to capture the domain scan. Upon receiving the data, a transformation process structures the received data into a more manageable form. This structured data is then updated for further use or storage. Error handling is robustly managed via normalization and updates post-error situations ensuring consistency and reliability in the output.

## Benefits
This automated component reduces manual intervention, speeds up the domain analysis process, and enhances the accuracy of threat assessments.

