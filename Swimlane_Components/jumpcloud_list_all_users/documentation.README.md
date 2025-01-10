This component streamlines the process of retrieving all Users from JumpCloud. Designed for workflows requiring comprehensive user data, it automatically handles pagination to fetch all results and outputs an array of objects. This enables seamless integration and efficient utilization of user data within your processes.



Usage:

- Install the component 
- Configure the filter as needed per your use case, by default it is empty which fetches all users. 
- Optional: A filter to apply to the query. 
  - Filter structure: <field>:<operator>:<value>. 
  - field = Populate with a valid field from an endpoint response. 
  - operator = Supported operators are: eq, ne, gt, ge, lt, le, between, search, in. 
  - value = Populate with the value you want to search for. Is case sensitive. Supports wild cards.
- Configure a JumpCloud asset with administrator privileges.
- Add to your playbooks to help automate any of your processes.

More information can be found at, https://docs.jumpcloud.com/api/1.0/#tag/Systemusers 

