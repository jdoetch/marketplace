# Rapid7 InsightVM - Create Tag - Technical Documentation

## Overview
This document provides technical details on the "Rapid7 InsightVM - Create Tag" component, outlining the functionalities, actions involved, and the flow process. It serves as a guide for end-users to understand and implement this component effectively in their environments, ensuring a smooth operation in asset management and security tagging within the Rapid7 InsightVM ecosystem.

## Component Summary
The "Rapid7 InsightVM - Create Tag" component is designed to facilitate the creation of asset tags within the Rapid7 InsightVM platform. This process helps in organizing, tracking, and applying security policies to various assets in a streamlined manner, enhancing the overall security posture and compliance management.

### Actions Overview
The component includes the following key actions:

#### Create Tag
- **Type**: Connector
- **Description**: Adds an asset and passes in the name and type inputs to generate a new asset tag.
- **On-success**: Proceeds to the Component Result.
- **On-failure**: There are no specific failure actions defined; the flow ends if this action fails.
- **Inputs**:
  - `json_body`: Contains the `name` and `type` of the tag to be created.
  - `verify_ssl`: A boolean input to verify SSL connections.

#### Component Result
- **Type**: Transformation
- **Description**: Holds the results of the Create Tag action and ensures the output is formatted correctly for further use.
- **Transformations**:
  - **Result**:
    - **Inputs**: Evaluates if the Create Tag action was successful. If not, it shows an error message.
    - **Processed Data**: Extracts and formats the result from the Create Tag action for display or further actions.

## Process Flow
1. **Start**: Initiation of the component.
2. **Create Tag Action**:
   - Inputs are taken (name and type of the tag).
   - Attempt to create the tag in Rapid7 InsightVM.
   - On success, moves to results transformation.
   - On failure, the process terminates.
3. **Component Result**:
   - Transformations are applied to format the output.
   - The final output is prepared for publishing or further usage.

## Conclusion
This component is essential for automating the asset management tasks in Rapid7 InsightVM, making it invaluable for maintaining an organized and secure asset database. The streamlined process of tagging ensures easy retrieval and management of assets, further enhancing the operational efficiency within the security management framework.

