# Fortinet FortiGate - Add Address to Network Address Group

## Overview
The Fortinet FortiGate - Add Address to Network Address Group is an automated component designed to facilitate the addition of network addresses into predefined address groups within FortiGate's security platform. This component efficiently assists in the systematic management and updating of network security parameters, ensuring enhanced security operations.

## Component Summary
This component primarily consists of interconnected actions that manage network addresses and their organization into groups on FortiGate systems. It is part of a larger system designed to simplify and automate the process of updating security assets to prevent unprotected entry points despite the dynamic nature of network addresses.

### Detailed Action Description:

1. **Get Group Members**
   - **Type:** Connector
   - **Purpose:** Retrieves the list of current members in a specified address group.
   - **On Success:** Proceeds to "Add New Address into Member List."
   - **On Failure:** Ends action.

2. **Add New Address into Member List**
   - **Type:** Python Script
   - **Purpose:** Adds a new address to the member list if it does not already exist within the group.
   - **Subsequent Steps:**
     - **On Success:** Proceeds to "Update Network Address Group."
     - **On Failure:** Ends action.

3. **Update Network Address Group**
   - **Type:** Connector
   - **Purpose:** Updates the network address group with the modified list of members that includes the newly added address.
   - **On Success:** Completes the process successfully.
   - **On Failure:** Ends action.

4. **Create IPv4 Address Object**
   - **Type:** Connector
   - **Purpose:** Creates a new IPv4 address object within FortiGate. Ensures continued progression of workflow even if object creation duplicates, leveraging existing objects.
   - **Subsequent Steps:**
     - **On Complete:** Triggers "Get Group Members" to update the group listing.

5. **Get Type by Version**
   - **Type:** Transformation
   - **Purpose:** Determines the type of address (IP mask or subnet) based on the FortiGate version.
   - **On Success:** Initiates the "Create IPv4 Address Object" action.

## Process Flow Summary
The process begins by identifying the type of network address based on the version of the FortiGate system. It then attempts to create an address object. Depending on the completion status of the address object creation, the system either moves forward to gather existing group members or stops if there is an issue.

If the group members are successfully fetched, it then checks and potentially adds the new address to the existing list. Upon successfully updating the member list, the system finalizes by updating the address group on FortiGate to include all recent changes, thereby achieving synchronization and updated security configurations.
