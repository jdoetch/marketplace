This Swimlane component enhances the functionality of the ArcherIRM connector by reformatting data retrieved through the “Get Records by Report ID” action. It transforms the associative field structure of the retrieved records into a key-value structure, ensuring compatibility with Swimlane workflows and enabling more efficient data utilization.

**Usage:**
- Create a new playbook
- Create a webhook trigger in the playbook 
- Import this ArcherIRM component into an action within the playbook
- Configure the “API Response” input of the webhook with the webhook json_body
- Hit the webhook endpoint with the following cURL command:
    - *curl --data "@./archer.json" "your_webhook_url"*
- The output of the component is now a loop-able set of key-value pairs