This Swimlane component enables users to selectively delete emails identified by their subject line within Microsoft Exchange. The component offers the flexibility to target a specific mailbox or perform a broader operation across all mailboxes in an organization. By automating the deletion process, it simplifies email management and supports compliance and security initiatives.

**Usage:**
- Create an asset for the Microsoft Exchange connector with the preferred method for authentication
- Create a playbook with a trigger and add the component to the playbook flow
- Assign the asset in the Delete Emails actions
- Configure inputs for the Delete Emails actions

**Inputs:**

- Subject: Subject of the email 
- Delete from all mailboxes: Accepts Boolean value, True or False 
- Delete Type: Soft or Hard delete 
- Mailbox Email Address: Required mailbox email if delete from all mailboxes is False 
- Dry Run: Accepts Boolean value, True or False 
- Ignore Exception: Accepts Boolean value, True or False 

**Outputs:**
- Results: JSON body result from delete email action 
- Status: status if successful or not

**Notes:**
- If all mailbox: checks if we need to delete the email from all mailboxes or not 
- Delete Emails from all mailboxes: delete emails from all mailboxes with a particular subject 

**Process Flow Summary:**
- Step 1: Initialize the variables Status and Result 
- Step 2: Check if Delete from all mailboxes is True or False
- Step 3: If Delete from all mailboxes is True, then use the Microsoft Exchange Delete Emails action to delete emails from all mailboxes, taking inputs as Subject. 
- Step 4: Update the variables Status and Result 
- Step 5: If Delete from all mailboxes is False then check if the mailbox address is defined 
- Step 6: If the mailbox address is defined, use the Microsoft Exchange Delete Emails action to delete emails from all mailboxes, taking inputs as Subject. 
- Step 4: Update the variables Status and Result 
- Step 7: If the mailbox address is not defined then Update the variables Status as mailbox address not defined and Result to empty