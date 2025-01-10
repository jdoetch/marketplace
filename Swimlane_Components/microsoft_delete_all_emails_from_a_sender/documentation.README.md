This Swimlane component enables users to manage emails from a specific sender within a designated account using the Microsoft Graph API. It provides functionality to list all emails from the sender for review and perform bulk deletion as needed. By automating these actions, the component supports efficient email management and enhances security workflows.

**Usage:**
- Create an asset for the Microsoft Graph connector with the preferred method for authentication 
- Create a playbook with a trigger and add the component to the playbook flow 
- Assign the asset in the List Emails and Delete Emails actions 
- Configure inputs for the List Emails and Delete Emails actions

**Inputs:**
- Account Email: Email associated with the User account 
- Email address: Sender Email we want to delete

**Outputs:**
- Results: Aggregate results

**Process Flow Summary:**
- Step 1: Get the Account email and Email addresses 
- Step 2: Send a request to Graph API to get all the emails sent to a particular user from a specified sender using the List Emails action 
- Step 3: Loop through List Emails action results parallelly to get the email ID 
- Step 4: Send a request to Graph API to delete the emails sent to a particular user with a specified email ID using the Delete Email action 
- Step 5: Send the aggregated results to output

