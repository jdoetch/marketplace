# SSC - Get Recent Generated Reports Component Documentation

## Overview
The SSC - Get Recent Generated Reports component automates the task of fetching recent reports from SecurityScorecard. It is structured to streamline the process of data retrieval and subsequent transformations for error handling and enrichment updates. This automation component aids in improving efficiency and accuracy of status checks and data enrichment related to cybersecurity performance metrics.

## Component Summary
The component consists of sequences of actions orchestrated to ensure a smooth transition from fetching recent reports to error normalization and enrichment updates. Here's a brief breakdown of each action:

### 1. Request Action
- **Type:** HTTP
- **Purpose:** Initiates the process by making an HTTP request to the SecurityScorecard API to fetch recent reports.
- **On Success:** Advances to Create Enrichment.
- **On Failure:** Moves to Normalize Create Error Action.

### 2. Create Variables Action
- **Type:** Create Variables
- **Purpose:** Sets up necessary variables for the process.
- **On Success:** Proceeds to Request Action.

### 3. Create Enrichment Action
- **Type:** Transformation
- **Purpose:** Transforms the response from the Request action based on predefined criteria.
- **On Success:** Triggers Update Enrichment Action.
  
### 4. Update Enrichment Action
- **Type:** Update Variables
- **Purpose:** Updates the variables with the newly created enrichment data.
- **On Success:** Completes if there are no subsequent actions.

### 5. Normalize Create Error Action
- **Type:** Connector
- **Purpose:** Handles errors from the Request Action by normalizing them.
- **On Success:** Proceeds to update Enrichment with the error details.

## Process Flow Summary
The component operates with a start from creating variables, then attempting to fetch recent reports via an HTTP request. Upon successfully fetching the data, it undergoes a transformation to formulate enrichment before updating this enrichment into the system. In cases where the HTTP request fails, the component normalizes the error and updates the enrichment correspondingly to ensure consistent handling of all outcomes.

