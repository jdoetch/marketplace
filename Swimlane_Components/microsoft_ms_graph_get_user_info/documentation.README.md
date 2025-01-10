# MS Graph - Get User Info Component Documentation

## Overview
The "MS Graph - Get User Info" component is designed to retrieve detailed information about a user within Microsoft Graph API, a unified API endpoint, for accessing Microsoft 365 services' data. This component is crucial in environments where user data needs to be fetched and manipulated for applications like user profile management, support ticketing systems, or employee directories.

## Component Summary
The "MS Graph - Get User Info" component connects to Microsoft Graph API to extract full user information. The component initiates a sequence of actions that begins with fetching user details and, based on the result, continues to parse the user information or handles errors if the fetch fails.

### Process Flow
1. **Fetch User Info**
   - **Type:** Connector
   - **Description:** Retrieves user information by user ID from Microsoft Graph API.
   - **On Success:** Triggers the "Parse User Info" action.
   - **On Failure:** Ends the flow with a failure status.

2. **Parse User Info**
   - **Type:** Python
   - **Description:** Processes the information fetched in a user-readable format, including user attributes like name, department, role, manager's details, etc.
   - **On Success:** Proceeds to "Update Record for Case."
   - **On Failure:** Ends the flow with a failure status.

3. **Update Record for Case**
   - **Type:** Record Action
   - **Description:** Updates a record within an application with the formatted user and leader information.
   - **On Complete:** Ends the process flow.

### Detailed Actions
- **Get User Info:**
  - **Purpose:** The primary action that fetches the data from Microsoft Graph API using the user’s unique identifier.
  - **Inputs:**
    - ID: User's unique identifier.
    - Select: Attributes to be fetched (city, company name, department, display name, job title).
    - Expand: To fetch nested attributes, like manager details (display name, job title, mail, id).

- **Parse User Info:**
  - **Purpose:** Converts raw data into a structured format by extracting and formatting user and manager information from the API response.
  - **Outputs:**
    - Formatted User Information
    - Direct Leader Information

- **Update Record for Case:**
  - **Purpose:** Utilizes formatted data to update specific fields in a case record within an application.
  - **Inputs:** Attributes like application name, tracking ID, new values to be patched, and fields to be appended or removed.

## Conclusion
The "MS Graph - Get User Info" component automates the retrieval and formatting of user information from Microsoft Graph, which can significantly improve efficiency in managing user data across business applications. The structured error handling and custom actions geared towards specific post-fetch operations make this component a valuable part of an IT or HR department's toolkit.
