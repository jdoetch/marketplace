# Fortinet FortiGate - Remove Domain From Network Address Group

## Overview
This technical document outlines the details of the Fortinet FortiGate - Remove Domain From Network Address Group component. This component facilitates the automated management of network address groups on Fortinet FortiGate devices, specifically the removal of domain objects from network address groups. Automation of this component enhances the overall security posture by ensuring immediate and consistent updates across the network infrastructure, reducing human error and maintaining compliance.

## Component Summary
The primary objective of this component is to automate the process of removing specific member domains from a configured network address group within the Fortinet FortiGate environment. This component is critical for dynamic security management where domains need to be quickly added or removed based on ongoing security analysis and threat management strategies.

### Actions Descriptions

#### Get Group Members
- **Type**: Connector
- **Purpose**: Retrieves the list of current members within a specific network address group. This action serves as a precursor to verifying and filtering out the domain to be removed.
- **Input Parameters**: Includes filters to specify the exact network address group by name.
- **Output**: List of current members.
- **On-Success**: Proceeds to the Remove Address from Member List.
- **On-Failure/On-Complete**: Error handling and logging are performed.

#### Remove Address from Member List
- **Type**: Python (Script)
- **Purpose**: Filters out the specific domain to be removed from the fetched list of group members.
- **Input**: Takes a custom domain as input and removes it from the list.
- **Output**: Updated list excluding the specified domain.
- **On-Success**: Triggers the Update Network Address Group action.
- **On-Failure/On-Complete**: Error handling and error-specific responses are managed here.

#### Update Network Address Group
- **Type**: Connector
- **Purpose**: Finalizes the removal process by updating the network address group with the new list of members (post removal).
- **Input**: The newly updated member list.
- **On-Success/On-Failure/On-Complete**: Provides confirmation of the update and handles any potential issues during the update.

## Process Flow
1. **Start**: Initiation of the action chain by specifying the target network address group.
2. **Get Group Members**: Fetches the existing list of domain names within the group.
3. **Remove Address from Member List**: Executes the script to exclude the specified domain from the list.
4. **Update Network Address Group**: Updates the group member list on the FortiGate device, confirming the removal of the domain.
5. **End**: Completes the operation with updated configuration.

This sequential flow ensures the process is handled efficiently and systematically, reducing the chances of discrepancies and maintaining the integrity of network configurations.

## Conclusion
The Fortinet FortiGate - Remove Domain From Network Address Group component is an essential tool for administrators looking to manage network security dynamically and efficiently. By automating this process, the component helps maintain high security and compliance standards while minimizing manual overhead and potential for error.

