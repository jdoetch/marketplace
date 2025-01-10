# Documentation: Rapid7 InsightVM - Get All Assets

### Overview
The "Rapid7 InsightVM - Get All Assets" component facilitates an efficient retrieval of all asset information within a network using the Rapid7 InsightVM technology. This component serves as a vital tool in managing asset security and ensuring comprehensive visibility across the network. By leveraging this component, organizations can automate the process of asset collection, enhance their security measures, and maintain up-to-date asset inventories.

### Component Summary
The "Rapid7 InsightVM - Get All Assets" component is designed to integrate smoothly with the Rapid7 InsightVM to fetch details on all assets available in the connected environment. It performs a crucial function by collecting comprehensive asset details, which are imperative for effective asset management and security compliance.

### Actions and Workflows
**Action: Get All Assets**
- **Type:** Connector
- **Description:** Retrieves a full list of assets from Rapid7 InsightVM. It allows optional inputs to refine the results based on page, size, and sorting parameters.
- **Inputs:**
  - **Page:** Specifies the page number of results to retrieve.
  - **Size:** Determines the number of assets per page.
  - **Sort:** Defines the criteria and order for sorting the asset list.
  - **Verify SSL:** A boolean to decide whether to verify SSL certificates while making requests.
- **Process Flow:**
  - **On Success:** Proceeds to the component result transformation phase.
  - **On Failure:** Ends the operation without proceeding.
  - **On Complete:** Finalizes the component execution by returning the result.

**Transformation Action: Component Result**
- **Type:** Transformation
- **Description:** Handles the transformation of the output data received from the Get All Assets action.
- **Process Flow:**
  - **On Success:** Outputs are successfully transformed and published.
  - **On Failure:** Transformation does not proceed, and component execution stops.
  - **On Complete:** Executes any final cleanup or post-execution steps if defined.

### Overall Process Flow Summary
1. **Initialization:** The component begins with the "Get All Assets" action, initiating a request to Rapid7 InsightVM.
2. **Data Retrieval:** Upon successful execution, asset data is fetched and passed to the subsequent transformation action.
3. **Data Transformation:** Here, any necessary transformation is applied to the retrieved data to suit the required output format.
4. **Conclusion:** The process either completes successfully, returning the formatted data, or halts due to an error during the data retrieval or transformation phase.

This detailed flow ensures that asset information is retrieved and processed effectively, contributing to improved security management and operational efficiency.

### Additional Considerations
- **Error Handling:** Proper error handling mechanisms are in place to address any issues during the connection, data retrieval, or data processing phases.
- **Security:** All communications are secured, with options to verify SSL certificates to prevent security risks associated with data interception.

This component is essential for organizations using Rapid7 InsightVM to enhance their asset management capabilities and maintain high standards of network security and compliance.

