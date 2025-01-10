# Tenable VM - Get Assets by IP or Hostname Component Documentation

## Overview
The "Tenable VM - Get Assets by IP or Hostname" component is designed to facilitate the retrieval of asset data from Tenable's Vulnerability Management platform using either an IP address or hostname as a query parameter. This component leverages HTTP protocols to query Tenable’s platform, aiming to provide seamless integration for users needing detailed insights into the security posture of specific assets within their networks.

## Summary of the Component
This component interacts with Tenable's API to fetch asset details. It is structured to handle requests asynchronously, ensuring effective handling of network responses and errors. The primary action within this component - "Enable Workbench Get Assets" - is responsible for initiating the API calls, handling success and failure scenarios, and parsing the response data to return it in a structured format.

## Detailed Action Overview
### Enable Workbench Get Assets
- **Type**: HTTP
- **Purpose**: To retrieve asset information from Tenable based on user-provided IP addresses or hostnames.
- **On-Success**: Continues to parse and format the data received.
- **On-Failure**: Logs the error and provides feedback to the user.
- **Inputs**:
  - **Endpoint**: Constructed URL to Tenable's API endpoint for workbenches/assets.
  - **Headers**: Includes credentials and API keys necessary for authentication.
  - **Query Parameters**: Filters to refine the search results, specifically by host target or match quality.
  - **Settings**: Configurations like follow redirects, verify certificates, and allowing unsafe legacy renegotiation are handled here.

## Overall Process Flow Summary
1. **Initialization**: The component starts with user inputs where they provide either an IP or hostname.
2. **API Interaction**: Using these inputs, the component constructs and sends a request to Tenable's API.
3. **Data Handling**:
   - On successful API interaction, the component parses the JSON response.
   - Formats the data for ease of use in the user’s system.
   - On failure, the component handles errors gracefully providing necessary error messages and logs.
4. **Completion**: Finally, the formatted data is either moved to another part of the system for further processing or sent back as a response to the initiating system.

This detailed, step-by-step documentation ensures that end-users can effectively integrate and utilize the "Tenable VM - Get Assets by IP or Hostname" component within their environments, maximizing their cybersecurity and asset management efforts.
