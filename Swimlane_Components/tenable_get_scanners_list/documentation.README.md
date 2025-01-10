# Tenable VM - Get Scanners List Technical Documentation

## Overview
The "Tenable VM - Get Scanners List" component is designed to interface with Tenable.io to retrieve a list of scanner appliances. This component plays a crucial role in ensuring that security teams have up-to-date information on available scanners for conducting vulnerability assessments.

## Component Summary
The "Tenable VM - Get Scanners List" component leverages a series of actions to interact with Tenable.io, perform data transformation, and output a refined list of scanner details. It is part of a larger automation system that enhances the efficiency and accuracy of vulnerability management processes.

### Actions Described

#### Enable Get Scanners List
- **Type**: Connector
- **Purpose**: This action initiates the connection to Tenable.io and requests a list of all available scanners.
- **On-Success**:
  - **Extract Scanner Details**: Triggered upon successful execution of the action.
- **On-Failure**: No subsequent steps defined.
- **On-Complete**: No subsequent steps defined.
- **Publish**: Outputs are not defined for publishing at this stage.

#### Extract Scanner Details
- **Type**: Transformation
- **Purpose**: Processes the JSON data fetched from Tenable.io, filtering and structifying the desired information about the scanners.
- **On-Success**: No subsequent steps defined; typically leads to a completion state or further custom actions in an extended component.
- **On-Failure**: No subsequent steps defined.
- **On-Complete**: No subsequent steps defined.
- **Publish**: The outputs include refined subsets of scanner data such as filtered scanner details and scanner counts.

### Overall Process Flow
The process begins with the action "Enable Get Scanners List", which fetches the scanners from Tenable.io. Upon successful execution, the process moves to the "Extract Scanner Details" action, which refines and structures the scanner information. This refined data is essential for further vulnerability management activities.

The design ensures that only relevant and necessary data is conveyed forward, maintaining system efficiency and relevancy. The data transformation leverages advanced JSONata expressions to filter and manipulate the raw scanner data.

## Conclusion
In summary, this component seamlessly integrates with Tenable.io, supplies critical data for vulnerability assessments, and ensures data is processed correctly for optimal use within the security infrastructure.

