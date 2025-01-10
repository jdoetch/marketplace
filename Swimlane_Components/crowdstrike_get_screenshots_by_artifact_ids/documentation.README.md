# Crowdstrike - Get Screenshot by Artifact IDs

## Overview

The "Crowdstrike - Get Screenshot by Artifact IDs" component leverages Crowdstrike's capabilities to automate the process of obtaining screenshots by using specific artifact IDs, enhancing incident response tasks and security workflows.

## Component Summary

This component consists of sequenced actions designed to efficiently gather screenshots from various artifacts identified within the Crowdstrike environment. It streamlines the process of collecting and analyzing visual data during security investigations, significantly reducing manual overhead and accelerating response times.

### Actions

#### 1. Loop Artifacts
- **Type:** Loop
- **Purpose:** Iterates over a list of artifact IDs provided as inputs.
- **On Success:** Proceed to download the screenshot.
- **On Failure:** Not specified.
- **On Complete:** Not specified.

#### 2. Download Screenshot
- **Type:** HTTP
- **Purpose:** Fetches screenshots from the Crowdstrike API for each artifact ID processed in the loop.
- **Inputs:** 
  - **Endpoint:** https://api.us-2.crowdstrike.com/falcon/entities/artifacts/v1
  - **Headers and Method:** Configured as per Crowdstrike API requirements.
  - **Query Parameters:** Parameter id set dynamically to each artifact's ID.
- **On Success:** Not specified.
- **On Failure:** Not specified.
- **On Complete:** Not specified.

#### 3. Transform
- **Type:** Transformation
- **Purpose:** Transforms the results received from screenshots to a specified format to be utilized or displayed.
- **On Success:** Not specified.
- **On Failure:** Not specified.
- **On Complete:** Not specified.

### Overall Process Flow
- **Start:** The process initiates by looping through each provided artifact ID.
- **Action:** For each artifact, a screenshot is downloaded using the HTTP API.
- **Transformation:** The raw data from each screenshot is transformed.
- **Completion:** The process either completes after all artifacts are processed, or stops upon encountering a failure if specified.

## Process Flow Diagram

Refer to the accompanying mermaid.txt file for a visual representation of the process flow.

## Configuration and Setup

- **Authentication:** Ensure proper OAuth configuration with Crowdstrike to authenticate API requests.
- **Parameters:** Customize query parameters and headers based on specific needs or changes in API.
- **Error Handling:** Set up error handling routines for potential API failures or data transformation issues.

## Conclusion

The "Crowdstrike - Get Screenshot by Artifact IDs" component is an essential tool for security operations, providing automated capabilities to retrieve necessary visual evidence swiftly. This automation component not only enhances efficiency but also supports comprehensive security investigations by ensuring quick access to pertinent data.
