# Microsoft Teams - Create One on One Session and Send User Chat Messages

## Overview
The "Microsoft Teams - Create One on One Session and Send User Chat Messages" component is designed to automate the process of setting up a one-on-one chat session within Microsoft Teams and subsequently sending messages within that session. This documentation details the workflow, actions, and configurations embedded within this component.

## Component Summary
This component automates tasks in Microsoft Teams through a series of actions that involve creating a chat, sending messages, and listing messages within that chat. Each action is designed to execute sequentially to facilitate a smooth operation ranging from session creation to message handling.

## Actions Description

### 1. Create Chat Session (`create_chat_auj_asv`)
- **Type**: Connector
- **Purpose**: Initiates a one-on-one chat session between two users specified in the inputs.
- **On-success**: Triggers the `send_message_to_chat_addzf_al` action.
- **Inputs**:
  - `json_body`: Contains the chat type and members involved in the chat.
  - Members are specified using their Microsoft unique identifiers and are assigned the role of 'owner'.

### 2. Send Message to Chat (`send_message_to_chat_addzf_al`)
- **Type**: Connector
- **Purpose**: Sends a message to the newly created chat session.
- **On-success**: Triggers the `list_messages_in_chat_ak_acnr` action.
- **Inputs**:
  - `path_parameters`: Utilizes the chat-id obtained from the chat creation result.
  - `json_body`: Contains the body of the message to be sent.

### 3. List Messages in Chat (`list_messages_in_chat_ak_acnr`)
- **Type**: Connector
- **Purpose**: Lists all messages within a specific chat session to verify successful message delivery.
- **On-success**: Triggers the `prepare_outputs` action.
- **Inputs**:
  - `path_parameters`: Utilizes the chat-id obtained from the chat creation result.

### 4. Prepare Outputs (`prepare_outputs`)
- **Type**: Transformation
- **Purpose**: Processes and formats the output of the listed messages for further use or verification.
- **Transformations**: Selectively extracts and formats message details such as display name, content, and creation datetime for clarity and further action.

## Overall Process Flow Summary
The execution flow of this component begins with the creation of a chat session followed by sending a message to this session, listing all messages to confirm the send, and finally preparing outputs for user verification or further processing. This automated series of actions simplifies communication management within Microsoft Teams, particularly enhancing direct interactions between users.

