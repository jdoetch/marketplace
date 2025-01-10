# API Void - IP Reputation Component Documentation

## Overview
The API Void - IP Reputation component is designed to assess the reputation of IP addresses via API Void’s external service, providing insights into potentially malicious activities associated with these IPs. This component is crucial in cybersecurity operations, specifically tailored for identifying IP addresses commonly used for spam, attacks on websites, or fraudulent activities. It utilizes HTTP requests to interact with the API Void service, verifying IP reputation in real time.

## Summary of the Component
The component "API Void - IP Reputation" is structured to execute a crucial security check against IP addresses by querying the API Void's IP reputation service. The process involves a series of steps executed based on the conditions met during the operation:
- **Process Flow**: If the call to the API emerges successfully, subsequent steps are considered, otherwise, alternative flows might be taken depending on the component’s configuration.

## Actions
### IP Reputation Check
- **Type**: HTTP (RESTful API call)
- **Purpose**: This action queries an IP address reputation using API Void's IP reputation service.
- **Endpoint**: `https://endpoint.apivoid.com/iprep/v/pay-as-you-go/`
- **Method**: GET
- **Headers**: Not specified
- **Query Parameters**:
  - `key`: ip
  - `value`: (dynamic IP address)
  - `description`: Enter the IP address to check its reputation.
- **Settings**:
  - `followRedirects`: true
  - `verifyCertificates`: true
  - `allowUnsafeLegacyRenegotiation`: false
- **On-Success Actions**: These are steps to be taken if the API call results in successful execution without errors.
- **On-Failure Actions**: These are steps to manage failures during the API call effectively.
- **On-Complete Actions**: These represent what should be done once the IP reputation check completes, regardless of success or failure.

## Process Flow Summary
The component's execution flow initiates with an IP address input, which is then processed through the API Void’s IP reputation service. Based on the response:
- If the reputation check completes successfully, the on-success actions will be undertaken.
- On encountering errors during the check, on-failure actions are triggered.
- Once the component completes the IP check, the on-complete actions are enacted as configured.

The essential purpose of this workflow is to provide users with a reliable method to assess the threat level associated with specific IP addresses, thereby enhancing the cybersecurity measures within their IT environment.

