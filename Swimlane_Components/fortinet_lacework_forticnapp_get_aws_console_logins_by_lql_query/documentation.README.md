# Technical Documentation: Lacework - Get AWS Console Logins by LQL Query

## Overview
This document provides comprehensive information on the component 'Lacework - Get AWS Console Logins by LQL Query', designed to interact with AWS services to capture and process console login events using Lacework's LQL (Lacework Query Language). This component primarily aims to enhance security measures by analyzing login activities, aiding in the detection and investigation of potential security incidents.

## Purpose of the Flow
The flow exists to automate the monitoring of AWS Console login events, transforming and normalizing data concerning these events, and subsequently updating alert databases. It leverages the power of Lacework for real-time security analysis and ensures efficient management of security alert systems.

### Summary of the Component
The component orchestrate actions, starting from querying AWS Console logins, transforming dates, creating necessary variables, normalizing alert formats, and finally updating alerts across the system. It is integrated within a Lacework environment and relies on seamless connectivity with AWS APIs.

### Actions Breakdown
#### 1. **Run LQL Query**
   - **Type:** Connector
   - **Description:** Executes an LQL query to retrieve AWS Console login events.
   - **Subsequent Steps:**
     - **On Success:** Normalize Alert
     - **On Failure:** No specific action defined.

#### 2. **Set Dates**
   - **Type:** Transformation
   - **Description:** Generates necessary date formats needed for filters in the LQL queries.
   - **Subsequent Steps:**
     - **On Success:** Run LQL Query
     - **On Failure:** No specific action defined.

#### 3. **Create Variables**
   - **Type:** Create Variables
   - **Description:** Establishes required variables for the process flow.
   - **Subsequent Steps:**
     - **On Success:** Set Dates
     - **On Failure:** No specific action defined.

#### 4. **Normalize Alert**
   - **Type:** Transformation
   - **Description:** Standardizes the alert data structure, preparing for update.
   - **Subsequent Steps:**
     - **On Success:** Update Alerts
     - **On Failure:** No specific action defined.

#### 5. **Update Alerts**
   - **Type:** Update Variables
   - **Description:** Updates the central alert database with normalized alert data.
   - **Subsequent Steps:**
     - **On Success:** No specific action defined.
     - **On Failure:** No specific action defined.

### Process Flow Summary
1. **Initialization:** Starts with initialization of variables required for the query.
2. **Query Execution:** Fetches data using an LQL query focused on capturing AWS Console login events.
3. **Data Transformation:** Dates are transformed to fit the needed criteria for analysis.
4. **Data Normalization:** Format and arrange the fetched data into a standardized alert schema.
5. **Data Updating:** Feed the normalized data back to the alert system, completing the flow cycle with successful monitoring and analysis of AWS Console logins.

The component operates continuously, ensuring real-time monitoring and quick updates to security alerts, aiding administrators in maintaining robust security protocols.

