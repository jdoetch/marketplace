# Microsoft Teams - Send Adaptive Card to One on One User Chat

## Overview
The Microsoft Teams - Send Adaptive Card to One on One User Chat component provides a streamlined process for sending dynamic, interactive Adaptive Cards directly to a one-on-one user chat in Microsoft Teams. This component forms part of automation workflows where personalized notifications or action-based communications are necessary.

## Component Summary
This component is crucial for situations requiring direct and interactive communication within Microsoft Teams, leveraging the Adaptive Card format to present information that is both rich in content and interactive functionality.

### Actions
#### Adaptive Card Object
- **Type:** Transformation
- **Purpose:** To construct the payload of the Adaptive Card with dynamic content and control structures before dispatch to a recipient in Teams.
- **On Success:**
  - Proceed to send the Adaptive Card message.
- **On Failure or On Complete:**
  - There are no further steps as this is typically the entry point.

#### Send Adaptive Card to One on One User Chat Message
- **Type:** Connector (Microsoft Teams)
- **Purpose:** To send the formatted Adaptive Card message to a specified user in Microsoft Teams via one-on-one chat.
- **Inputs:**
  - Uses the `chat-id` to identify the user to whom the message will be sent.
  - Adaptive Card content from the transformation action.
- **On Success, On Failure, On Complete:**
  - No subsequent actions are defined; this is the exit point of the component.

## Overall Process Flow Summary
1. **Adaptive Card Construction:** Initiate with constructing the Adaptive card dynamically based on input parameters such as user data and control needs.
2. **Dispatching the Card:** Once the card is successfully created and dynamically filled with content, it's ready to be sent. This is done through a connector that interfaces directly with Microsoft Teams to send the message to the intended recipient.
3. **Completion:** The process either completes successfully, ensuring the recipient receives the card, or fails, in which case error handling mechanisms should address the failure based on predefined criteria.

### Reason for Existence
This component exists to facilitate personalized and direct communication within Microsoft Teams, using the capabilities of Adaptive Cards to engage users interactively and effectively in one-on-one chats. It helps in automating responses and actions directly within a familiar chat environment, improving operational efficiency and user interaction.

### Technical Details
- **Dependencies:** Requires a Microsoft Teams integration set up with proper authorization to send messages.
- **Limitations:** Relies on proper formatting and dynamic data provision for the Adaptive Cards to ensure they render correctly on the recipient's device.
- **Security:** All communications are secured through standard Microsoft Teams security protocols.

@author Microsoft and Swimlane
