# Cortex - Terminate GlobalProtect Connections

## Overview
The "Cortex - Terminate GlobalProtect Connections" component automates the termination of active GlobalProtect VPN connections within an enterprise network. This automated flow aims to enhance security measures by swiftly disconnecting endpoints that may pose a security threat or are no longer authorized.

## Component Summary
The component executes a sequence of orchestrated actions to identify and disconnect specific GlobalProtect VPN sessions using Palo Alto Networks technologies. It leverages actions like user identity verification, session status checks, and direct termination commands.

### Actions and Processes
1. **Create Component Variables**:
   - **Purpose**: Initiates the component by setting up necessary variables.
   - **Type**: Variable creation
   - **On Success**: Executes a parallel action group.
   - **On Failure**: None specified.

2. **Parallel Action Group**:
   - **Purpose**: Executes multiple actions concurrently to determine the user and session details.
   - **Type**: Parallel group
   - **On Success**: Triggers a no-operation action.
   - **On Failure**: None specified.

3. **Find User by Endpoint**:
   - **Purpose**: Retrieves details about the user using the hostname parameter to identify the session.
   - **Type**: Data retrieval
   - **On Success**: Checks if the endpoint is found.
   - **On Failure**: Creates a status call failed action.
   
4. **Check If Endpoint Is Found**:
   - **Purpose**: Conditionally checks the outcome of the user search and either proceeds with further actions or flags the user as not found.
   - **Type**: Conditional check
   - **On Success**: None specified.
   - **On Failure**: Flags the endpoint as not found.

5. **Update Result (Error)**:
   - **Purpose**: Updates variables based on failure scenarios, such as an unsuccessful user identification or session validation.
   - **Type**: Variables update
   - **On Success**: None specified.
   - **On Failure**: None specified.

6. **Prepare Firewall Call**:
   - **Purpose**: Prepares and transforms data for a firewall call to terminate the VPN session.
   - **Type**: Data transformation
   - **On Success**: Adds user to block list.
   - **On Failure**: None specified.

7. **Add User to Block List**:
   - **Purpose**: Executes a task on a firewall to block or terminate the user session by interacting with the Palo Alto Networks firewall.
   - **Type**: External system interaction
   - **On Success**: Extracts and evaluates the result.
   - **On Failure**: Initiates an error handling action.

8. **Extract Call Result**:
   - **Purpose**: Analyzes the result returned from the firewall and determines the success or failure of the session termination.
   - **Type**: Data transformation
   - **On Success**: Finalizes the session termination as successful.
   - **On Failure**: Extracts error message details.

9. **Final Status Update**:
   - **Purpose**: Updates the final status of the operation indicating success or detailed error messages.
   - **Type**: Status update
   - **On Success**: None specified.
   - **On Failure**: None specified.

## Overall Process Flow Summary
The component follows a comprehensive process to manage and terminate VPN sessions securely:
1. Initialize variable settings.
2. Concurrently fetch user details and verify session status.
3. Validate endpoint data and either proceed with termination or mark as not found.
4. Update internal statuses based on operation outcomes.
5. Execute firewall interactions to block the user, followed by detailed result analysis.
6. Conclude the operation with a definitive status update.

By employing these steps, the "Cortex - Terminate GlobalProtect Connections" component ensures that only authorized sessions remain active, thereby fortifying the network security infrastructure.

