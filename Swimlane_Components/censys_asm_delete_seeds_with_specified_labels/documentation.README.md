# Censys ASM - Delete Seeds with a Specified Label
## Short Description
The "Censys ASM - Delete Seeds with a Specified Label" component is designed to automate the process of deleting seeds from the Censys ASM platform based on a specified label. This component is essential for maintaining the cleanliness and relevance of data within enterprise security environments that use Censys ASM.

## Summary
This component interacts with the Censys ASM API to selectively delete seeds tagged with a particular label. It handles various states such as active, fail, queued, and success to ensure robust management of these seeds.

### Process Flow Summary
1. **Initialization**: The component begins by creating necessary variables for the operation.
2. **HTTP Request Execution**: Executes an HTTP request to the Censys ASM API endpoint to fetch seeds with the specified label.
3. **Enrichment Creation & Update**: Based on the response from the API, it creates and updates enrichment data related to the seeds.
4. **Error Handling**: In case of request failure, the component normalizes error data and updates the enrichment accordingly.
5. **Completion**: On successful deletion, the process ends, and in the case of failure, it handles the errors accordingly.

### Detailed Action Descriptions
#### Create Variables
This action initializes the required variables for processing the deletion.
- **Type**: create_variables
- **On-Success**: Proceed to send an HTTP request.
- **On-Failure**: End the process with an error status.

#### Send HTTP Request
This sends a request to Censys ASM API to fetch the seeds with a specific label.
- **Type**: http
- **Input**: Label of seeds to delete
- **On-Success**: Proceed to create enrichment.
- **On-Failure**: Trigger error normalization.

#### Create Enrichment
Based on the data retrieved, it structures the enrichment details.
- **Type**: transformation
- **On-Success**: Update enrichment.
- **On-Failure**: Log and handle the error.

#### Normalize Request Error
Normalizes and logs the error information received from the Censys ASM API.
- **Type**: connector
- **On-Success**: Update enrichment with error details.
- **On-Failure**: End the process marking failure.

#### Update Enrichment
Updates the enrichment data with new or corrected information post-initial creation.
- **Type**: update_variables
- **On-Success**: Complete the process on a high note.
- **On-Failure**: Retry or end with failure status.

### Conclusion
The "Censys ASM - Delete Seeds with a Specified Label" component effectively manages and automates the deletion of labeled seeds within Censys ASM, ensuring operational efficiency and data accuracy in security operations.

