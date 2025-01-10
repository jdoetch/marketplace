This Swimlane component retrieves and organizes a list of contacts from the Staffbase Email Contacts Directory using the "Get All Contacts" action. Designed to streamline contact management and integration into workflows, this component provides a structured and accessible list of staff email contacts for use in automation, reporting, and communication processes.

**Usage:**
- Configure the assets on StaffBase Keys 
- Add the desired inputs on the Get Contact List HTTP action under the body tab, only edit the values if needed (don’t edit the properties)
- Add the component to a Playbook workflow 
- Get users returned as an array for further usage

**Inputs:**
- limit (optional, defaults to 100): The amount of items that should be returned.
- offset (optional, defaults to 0): Define an offset for getting the items starting at this number.
- orderBy (optional): Must define field and type of order (DESC/ASC).