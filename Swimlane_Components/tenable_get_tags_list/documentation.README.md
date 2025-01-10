# Tenable VM - Get Tags List

## Overview of Tenable VM - Get Tags List
Tenable VM - Get Tags List is a component designed to facilitate the retrieval and management of tags within the Tenable VM environment. The main purpose of this component is to allow users to efficiently query and manipulate tag data associated with their vulnerability management processes. This document provides detailed technical documentation aimed at assisting end-users in understanding and utilizing this component effectively.

## Component Summary
This component is structured to query Tenable VM to retrieve a list of tags based on specified criteria. It supports numerous parameters and settings which allow for customization according to the user's needs, ensuring flexibility and powerful querying capabilities.

## Actions
### Enable Get Tags
#### Action Type: HTTP
#### Purpose:
The "Enable Get Tags" action serves as the primary mechanism through which tag data is retrieved from Tenable VM. It interacts with Tenable's API using HTTP calls, formatted to meet the API's request structure.

#### Inputs:
- **Endpoint**: The URL endpoint for the Tenable VM API (tags/values).
- **Method**: HTTP method used (typically GET).
- **Headers**: Includes authorization headers generated dynamically using assets.
- **Query Parameters**: Supports various parameters like wildcard search which allows filtering of tags based on specific criteria.
- **Settings**:
  - **Follow Redirects**: Boolean indicating if redirects should be followed.
  - **Verify Certificates**: Boolean indicating if SSL certificates need to be verified.
  - **Allow Unsafe Legacy Renegotiation**: Boolean flag for legacy TLS negotiation.

#### Outputs:
- **Path**: JSON endpoint where results are published.
- **Result Body**: Contains tags returned from API along with pagination information to assist in result management.

#### Flow:
1. **On Success**: Data is published to specified output path.
2. **On Failure**: Error handling messages or logs are generated.
3. **On Complete**: Final step cleanup or additional logging.

## Process Flow Summary
1. **Initialization**: Component is initialized with necessary configuration and authentication.
2. **Tag Querying**: Executes "Enable Get Tags" action to send an HTTP request.
3. **Response Handling**: Processes the response from Tenable VM. Success or failure paths are taken based on the response status.
4. **Output Management**: On successful retrieval, tag data along with pagination information is published to configured endpoints.
5. **Completion**: Final steps or cleanup operations are executed.

## Summary
By leveraging the "Tenable VM - Get Tags List" component, users can streamline the process of managing tags associated with their assets in Tenable VM, improving both efficiency and oversight in their vulnerability management processes.

