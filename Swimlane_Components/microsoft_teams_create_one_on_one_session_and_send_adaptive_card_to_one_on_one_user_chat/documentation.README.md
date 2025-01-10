# Microsoft Teams - Create One on One Session and Send AdaptiveCard to One on One User Chat

## Overview

The "Microsoft Teams - Create One on One Session and Send AdaptiveCard to One on One User Chat" component is designed to streamline communication within Microsoft Teams by enabling automated creation of one-on-one chat sessions and sending customized AdaptiveCards within these sessions. This component is vital for enhancing user interaction through automated processes, suitable for HR announcements, IT helpdesk interactions, or quick updates within organizations.

## Component Summary

This technical document outlines the functionalities of automating Microsoft Teams tasks related to chat and information sharing. The component consists of several interconnected actions that ensure the seamless execution of chat session creation and message dissemination using AdaptiveCards.

### Process Flow

1. **Create Chat:** Initiates a new one-on-one chat session.
2. **Send Message to Chat:** Follows the creation of the chat; sends an AdaptiveCard as a message to the newly created chat session.
3. **List Messages in Chat:** Optionally lists all messages in a chat to verify the message was sent successfully.
4. **Transformation of Data:** Handles any data transformation required for the AdaptiveCard content.
5. **Prepare Output:** Final step to format and prepare the output after the main actions have completed.

### Actions Described

- **Create Chat**
  - **Type:** Connector
  - **Purpose:** Starts a new one-on-one chat between users.
  - **On-Success:** Proceeds to the README action.
  - **On-Failure:** There are no subsequent steps defined for failure; however, error handling is implied.

- **Send Message to Chat**
  - **Type:** Connector
  - **Purpose:** Sends an AdaptiveCard to the created chat session.
  - **On-Success:** Triggers the listing of messages in the chat to confirm delivery.
  - **On-Failure:** Error handling or retry logic would typically follow here.

- **List Messages in Chat**
  - **Type:** Connector
  - **Purpose:** Confirms that the AdaptiveCard was sent by listing all messages in the chat.
  - **On-Success:** Leads to Prepare Output action.
  - **On-Failure:** Not specified; assume error logging or alerting.

- **Transformation**
  - **Type:** Transformation
  - **Purpose:** Transforms the input data into a format suitable for the AdaptiveCard.
  - **On-Success:** Passes the transformed data to the send message action.

- **Prepare Output**
  - **Type:** Transformation
  - **Purpose:** Formats and prepares the final output after the AdaptiveCard has been successfully sent.
  - **On-Success:** Completes the process flow.

### Overall Process Flow Summary

The component automates a sequence where a chat is created, a message in the form of an AdaptiveCard is prepared and sent, and the outcome is verified through a series of connected actions. This organization not only ensures efficiency but also maintains a high standard of data integrity and interaction quality within Microsoft Teams environments.

## Conclusion

The component "Microsoft Teams - Create One on One Session and Send AdaptiveCard to One on One User Chat" encompasses crucial features for enhancing direct communication and workflow automation within organizations using Microsoft Teams. By detailing each step and its functionalities, this guide serves as a comprehensive resource for understanding and implementing this automated sequence efficiently.

