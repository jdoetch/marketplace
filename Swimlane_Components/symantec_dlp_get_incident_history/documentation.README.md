# Symantec DLP - Get Incident History Component Documentation

## Overview
This documentation details the functionality and usage of the "Symantec DLP - Get Incident History" component within an enterprise setup. This component is crucial for organizations that rely on Symantec's Data Loss Prevention (DLP) solutions to monitor and manage data security across their IT environments.

## Short Description
The purpose of the "Symantec DLP - Get Incident History" component is to retrieve a detailed incident history related to data security events captured by Symantec DLP. This component interfaces with Symantec DLP through specified connectors and inputs, allowing users to fetch comprehensive incident logs crucial for analysis and compliance tracking.

## Component Actions Overview
### Get Incident History Action

#### Type
- **Connector**

#### Description
This action initiates a connection to Symantec DLP to retrieve the incident history by using the incident ID provided through the action inputs.

#### Inputs
- **path_parameters**: Includes `id` which refers to the incident ID.
- **verify_ssl**: A boolean value to decide whether to verify SSL certificate.

#### Success Scenario
On successful retrieval of the data, the action proceeds to the component result transformation stage without any intermediate actions.

#### Failure Handling
In case of failure, no specific actions are defined, and the process ends without proceeding further.

#### Completion Handling
- **Component Result**: This section is triggered upon the completion of the incident history retrieval offering transformation functionalities for the fetched data.

## Transformation: Component Result

#### Type
- **Transformation**

#### Purpose
The purpose of this transformation step is to process the retrieved incident data, making it suitable for further utilization or reporting.

#### Transformation Details
The result transformation checks for data existence and modifies the presentation based on the fetched incident history. It helps in conditioning the output for end-users, providing flexibility in displaying the results.

## Overall Process Flow Summary
1. **Initialize**: The component begins with receiving the incident ID as an input.
2. **Get Incident History**: Connects to Symantec DLP using the specified parameters and seeks to retrieve the corresponding incident history.
3. **Process Results**: Upon fetching the data, the transformation action processes it to match the desired output format.
4. **Complete Action**: After the transformation, the results are finalized for presentation or further actions as configured.

This process enables organizations to routinely fetch and audit their incident logs through a robust, automated component, ensuring adherence to data governance and compliance standards.

