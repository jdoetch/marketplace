# Fortinet FortiGate - Add Domain to Network Address Group

## Overview
This document provides a comprehensive guide on using the "Fortinet FortiGate - Add Domain to Network Address Group" component. The primary purpose of this component within an automated environment is to dynamically update network security configurations by adding a domain to an existing network address group in FortiGate firewalls. This process is vital for security operations, ensuring network changes are instantly reflected in security settings, minimizing gaps and maintaining strict access controls.

## Detailed Process Flow and Actions

### Create Domain Address Object
- **Type**: Connector
- **Purpose**: This action initiates the flow by creating a domain address object in FortiGate using the domain details provided.
- **Subsequent Steps**: 
  - **On Success**: Proceeds to Get Group Members.
  - **On Failure**: None defined, implying that the flow halts on failure.

### Get Group Members
- **Type**: Connector
- **Purpose**: Retrieves the current list of members in a specified network address group from FortiGate.
- **Subsequent Steps**:
  - **On Success**: Add New Address into Member List.
  - **On Failure**: None defined, suggesting that an error might terminate the process.

### Add New Address into Member List
- **Type**: Python Script
- **Purpose**: This action involves executing a Python script that checks for the existence of the new domain in the retrieved member list. If the domain is not present, it is added.
- **Subsequent Steps**:
  - **On Success**: Update Network Address Group.
  - **On Failure**: None defined, indicating script robustness or criticality of action success.

### Update Network Address Group
- **Type**: Connector
- **Purpose**: Updates the network address group with the new member list, effectively adding the domain to the group.
- **Subsequent Steps**:
  - **On Success**: None defined.
  - **On Failure**: None specified.

## Overall Process Summary
The component "Fortinet FortiGate - Add Domain to Network Address Group" automates a critical security operation by updating network address groups dynamically. This capability supports prompt adjustments to the network's security posture in response to operational needs without manual intervention. The actions involved include creating a domain address object, fetching the existing member list, possibly adding a new domain, and updating the group information in the FortiGate firewall.

## Key Benefits
- **Automated Security Management**: Ensures all changes are consistently applied across the network, reducing human error.
- **Real-Time Updates**: Minimizes security gaps by updating groups in real-time.
- **Scalability**: Handles changes dynamically to support growing organizational needs.

These features highlight its importance in modern, dynamic network environments requiring agile and robust security management systems.
