# Technical Documentation: Microsoft Active Directory (On-prem) - Disable User

## Overview
The Microsoft Active Directory (On-prem) - Disable User component is crafted to automate the process of disabling a user account within an on-premises Active Directory environment. This document outlines the structure, functionality, and flow of actions within this component.

## Purpose
Organizations require swift and reliable methods to modify user account statuses in response to various operational or security needs. The process of disabling user accounts is crucial for swiftly revoking access when required, which helps in maintaining overall IT security and operational integrity.

## Component Summary
This component interfaces with LDAP services to search, verify, and modify the attributes of user accounts in Active Directory. It automates the tasks to reduce manual effort and potential human errors, ensuring that access control changes are handled efficiently and without delay.

### Process Flow
The core actions of the component follow a structured path:
1. **Initialization**: Create necessary variables and setup.
2. **User Search**: Conduct LDAP search based on input criteria to locate the user.
3. **Account Validation**: Check if the account exists and validate the need to disable.
4. **Modify Account**: Execute LDAP modify operation to update the status of the user account to disabled.
5. **Status Update**: Record the success or failure of the operation.

### Detailed Action Descriptions
- **Create Component Variables**
  - **Type**: Create Variables
  - **Purpose**: Initializes the workflow by creating and configuring necessary variables and inputs.
  - **On-Success**: Proceeds to search for the user account.
  - **On-Failure**: Logs an error and terminates the process.

- **Parallel Actions Workflow**
  - **Type**: Parallel Group
  - **Purpose**: Manages multiple threads to efficiently handle operations like user searches and data processing concurrently.

- **Find Account**
  - **Type**: LDAP Search Connector
  - **Purpose**: Searches the Active Directory using provided LDAP attributes to locate the user account.
  - **On-Success**: Transitions to account counting to validate existence.
  - **On-Failure**: Creates a failure status and terminates the process.

- **Account Count**
  - **Type**: Data Transformation
  - **Purpose**: Validates the presence and the correct number of accounts found.
  - **On-Success**: Continues to disable the account if conditions are met.
  - **On-Failure**: Logs an error.

- **Disable or Enable Account**
  - **Type**: LDAP Modify Connector
  - **Purpose**: Modifies the user account control attributes to disable the user.
  - **On-Success**: Generates a success status update.
  - **On-Failure**: Logs the failure and ends the process.

- **Create Status (Success or Failed)**
  - **Type**: Variable Update
  - **Purpose**: Updates the workflow status based on the outcome of the account modification.
  - **On-Success**: Ends the workflow with a status report.
  - **On-Failure**: Logs an error.

## Conclusion
The Microsoft Active Directory (On-prem) - Disable User component ensures reliable execution of user disable operations on Active Directory systems, which is essential for maintaining secure and compliant IT environments. Effective automation reduces manual workload, promotes faster response times, and enhances security protocols.

