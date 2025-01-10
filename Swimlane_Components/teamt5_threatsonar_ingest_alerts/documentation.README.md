# ThreatSonar - Ingest Alerts Component Documentation

## Overview
The "ThreatSonar - Ingest Alerts" component is designed to automate the process of ingesting and processing alerts from endpoints within a security environment. This document provides a detailed overview of the component's capabilities, including each action, its purpose, types, and the overall flow.

### Component Summary
This component amalgamates various functionalities essential for handling endpoint security alerts. It primarily focuses on fetching, transforming, and analyzing endpoint data, followed by generating actionable insights and alerts.

### Detailed Process Flow and Actions
#### 1. Data Transformation
- **Type**: Transformation
- **Purpose**: Transforms received data(i.e., Event Start Time) into a usable format.
- **On-Success**: Triggers the action to list endpoints.
 
#### 2. List Endpoints
- **Type**: HTTP
- **Purpose**: Retrieves a list of all active endpoints from the ThreatSonar API.
- **On-Success**: Proceed to count endpoints.

#### 3. Loop Endpoints
- **Type**: Loop
- **Purpose**: Iterates through every single endpoint fetched.
- **On-Success**: Generates event details for each endpoint.

#### 4. Get Event Details
- **Type**: Connector (teamt_threatsonar_edr)
- **Purpose**: Fetches detailed events associated with a particular endpoint.
- **On-Success**: Connects and gets event connections.

#### 5. Get Event Connections
- **Type**: Connector
- **Purpose**: Acquires connected event information for deeper insights.
- **On-Success**: Transforms event data.

#### 6. Transform Event Data
- **Type**: Transformation
- **Purpose**: Manipulates and structures event data into a standardized format.
- **On-Success**: Loop back to process more endpoint data or finish process.

#### 7. Process Endpoint Data
- **Type**: Python
- **Purpose**: Executes customized scripts to filter and synthesize endpoint data based on specific conditions.
- **On-Success**: Parses observable elements relevant to security.

#### 8. Filter and Parse Observables
- **Type**: Connector
- **Purpose**: Identifies and extracts essential observables from endpoint data.
- **On-Success**: Create alerts based on the identified observables.

#### 9. Create Alert
- **Type**: Connector
- **Purpose**: Generates alerts in TEDS format, categorized by the severity and type of the detected incidents.
- **On-Complete**: Concludes the actions for the component or loops back for additional processing as needed.

### Overall Process Flow
Starting from transforming raw data, this component interfaces with various endpoints. Upon successful data retrieval, it branches into detailed event and connection analysis, followed by tailored data processing scripts and observable extraction, concluding with alert generation.

This flow ensures a comprehensive approach to endpoint security management by analyzing data at each point and making decisions based on real-time insights.

