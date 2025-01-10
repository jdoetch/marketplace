# Tenable VM - Get Policy List Component Documentation

## Overview
The "Tenable VM - Get Policy List" component is a sophisticated automation tool designed to streamline the process of retrieving policy lists from Tenable VM, a popular vulnerability management platform. This component is essential for organizations aiming to enhance their security posture by efficiently managing and auditing their security policies.

## Summary
This component integrates with Tenable VM through specified connectors, enabling users to list all policies currently in effect. The primary purpose is to facilitate the automation of security operations, making the management of vulnerability policies more effective and less resource-intensive.

### Process Flow
1. **Initiation**: The component initiates by activating the enable_list_policies action.
2. **Action Execution**:
    - **List Policies**: The enable_list_policies action connects to Tenable VM via a connector and requests a list of all policies. 
       - **On Success**: The flow proceeds to extract_policy_details.
       - **On Failure**: The flow ends, and error handling procedures are invoked.
3. **Data Transformation**:
    - **Extract Policy Details**: This action transforms the obtained policies data to filter and structure it according to the needs.
       - **Filtered Policies**: This step filters out the policies based on specified criteria, potentially reducing the volume of data.
       - **Policies Count**: Computes the size of the filtered policies to provide quick insights into the data volume managed.
4. **Completion**:
    - The final data set includes both detailed and summarized views of the policies, which can be used for reporting or further processing.

### Actions Description
- **enable_list_policies**:
  - **Type**: Connector
  - **Purpose**: Connects to Tenable VM and retrieves a list of all policies.
  - **On-Success**: Triggers extract_policy_details.
  - **On-Failure**: Terminates the process and triggers error handling.

- **extract_policy_details**:
  - **Type**: Transformation
  - **Purpose**: To filter and count the policies based on the obtained list from the initial action.
  - **Outputs**:
    - **Filtered Policies**: Contains policies that meet specific criteria.
    - **Filtered Policies Size**: The count of the filtered policies, providing a quick overview of the subset size.

## Overall Process Flow Summary
The component "Tenable VM - Get Policy List" begins with listing policies from Tenable VM, followed by detailed extraction and counting of relevant policy data. This dual-step process ensures that end-users have access to both raw and summarized data, enabling effective policy management and reporting.

### Benefits of Using This Component
- **Automation Efficiency**: Automates the tedious task of gathering policy data manually.
- **Security Enhancement**: Helps in quickly identifying and managing policies, contributing to the overall security framework.
- **Data Insight**: Provides both detailed and summary insights into the policies, aiding in decision-making processes.

This technical document should serve as a comprehensive guide for setting up and utilizing the "Tenable VM - Get Policy List" component within your security operations workflow.

