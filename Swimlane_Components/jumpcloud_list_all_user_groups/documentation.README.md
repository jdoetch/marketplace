This component streamlines the process of retrieving all User Groups from JumpCloud. Designed for workflows requiring comprehensive group data, it automatically handles pagination to fetch all results and outputs an array of objects. This enables seamless integration and efficient utilization of group data within your processes.

 

Usage:

- Install the component
- Configure the filter as needed per your use case, by default it is empty which fetches all groups.
- Optional: A filter to apply to the query. 
  - Filter structure: <field>:<operator>:<value>. 
    - field = Populate with a valid field from an endpoint response. 
    - operator = Supported operators are: eq, ne, gt, ge, lt, le, between, search, in. 
    - value = Populate with the value you want to search for. Is case sensitive. Supports wild cards.

- Configure a JumpCloud asset with administrator privileges.
- Add to your playbooks to help automate any of your processes.