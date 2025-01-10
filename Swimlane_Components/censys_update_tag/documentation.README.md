# Censys - Update Tag - Technical Documentation

## Overview

The "Censys - Update Tag" component is designed for effective tag management within the Censys platform. Its primary function is to facilitate the updating and enrichment of tags based on a set of defined automation rules. This component ensures that data tagging is both dynamic and aligned with the most current assessment or contextual changes.

## Summary

The "Censys - Update Tag" component achieves its objective through a series of coordinated actions. It begins with variable creation, proceeds to enrichment updates, and finally handles potential errors or updates the enrichment data before concluding the process flow.

## Process Flow and Actions Detailed Description

### 1. Create Variables

**Type:** Variable Creation  
**Purpose:** To initialize variables needed for further actions in the component.  
- **On Success:** Proceeds to the "Update Tag".
- **On Failure:** Workflow is halted.
- **Inputs:** Primary enrichment data elements.

### 2. Update Tag

**Type:** Connector (API call to Censys)  
**Purpose:** To update a tag in Censys with newly provided information.  
- **On Success:** Initiates the "Create Enrichment".
- **On Failure:** Executes "Normalize Great Error Data" to handle the error.
- **Inputs:** Tag ID, name, and metadata such as color.

### 3. Create Enrichment

**Type:** Transformation  
**Purpose:** To transform the response data from the "Update Tag" action into a structured format for further processing.  
- **On Success:** Leads to "Update Enrichment".
- **On Failure:** Terminates the flow.
- **Inputs:** Data derived from the "Update Tag" action results.

### 4. Update Enrichment

**Type:** Variable Update  
**Purpose:** To set the final enrichment data produced by the "Create Enrichment" action.  
- **On Success:** Concludes the process and possibly queues further related processes.
- **On Failure:** Ceases any subsequent operations.

### 5. Normalize Great Error Data

**Type:** Connector  
**Purpose:** To provide a normalized output for errors encountered during the "Update Tag" step, ensuring consistent error handling.
- **On Success:** Redirects to "Update Enrichment".
- **On Failure:** Ends the workflow.

## Process Flow Summary

The overall flow initiates with setting up necessary variables, followed by an attempt to update a tag. Depending on the outcome, it either progresses to enhancing the data enrichment or handling exceptions if the update fails. The component ensures that enrichment data is either successfully updated or properly handled in the case of errors, maintaining a streamlined operational stride for tag management in Censys.

