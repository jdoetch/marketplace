# Tenable VM - Get Folders List Component Documentation

## Overview
The Tenable VM - Get Folders List component is a crucial part of managing vulnerability assessment within network environments. It automates the retrieval of folder structures in Tenable VM, a popular network security management tool, facilitating better organization and efficient access to various reports and analyses stored within Tenable VM environments.

## Purpose
The component facilitates the automated retrieval of folder lists from Tenable VM, aiding users in effectively managing their security assessments and categorizing information without manual intervention.

## Component Actions
Below are the detailed actions included in the Tenable VM - Get Folders List component:

### 1. Enable Get Folders
- **Type:** Connector
- **Purpose:** Initiates the retrieval of folder lists from Tenable VM.
- **On-Success:** Triggers the Tract Folder Details action to further process the data.
- **On-Failure:** (No specific failure scenario captured, ensure proper error handling in implementation)
- **Description:** Connects to Tenable VM to fetch the list of folders using specified API credentials.

### 2. Tract Folder Details
- **Type:** Transformation
- **Purpose:** Processes the fetched folder data into a refined format.
- **On-Success:** (Proceeds to next set action or concludes if none)
- **On-Failure:** (No specific failure scenario captured, ensure proper error handling)
- **Description:** Transforms the data into a structured format that can be used for further actions or reporting.

## Published Data
- **Folders:** The raw list of folders fetched from Tenable VM.
- **Filtered Folders:** Refined and processed folders data post initial fetch.
- **Folder Size:** The count of total folders available.
- **Filtered Folder Size:** The count of folders after specific filtering.

## Process Flow Summary
The component works in a sequential manner:
1. Initiates by connecting to Tenable VM to fetch the current list of folders.
2. On successful fetch, the data is passed to the transformation step where folders are processed and refined for usability.
3. The detailed information regarding the number of folders (both raw and processed) is made available after the completion of data processing.

This automated flow ensures that at every point of success, there is a deliberate action to refine and structure the data, adding value and clarity to the information received from Tenable VM.

## Why This Flow Is Essential
Automating the process of fetching and organizing folder lists from Tenable VM drastically reduces manual oversight and labor involved in security management, making it an essential tool in continuous vulnerability assessment and data organization strategies.

