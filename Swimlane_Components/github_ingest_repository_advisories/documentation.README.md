This Swimlane component automates the ingestion of security advisories from GitHub repositories and transforms them into actionable TEDS alert objects to interface with Swimlane’s SOC Solution. It ensures timely and seamless integration of GitHub's vulnerability insights, enabling enhanced threat monitoring and response.

**Usage:**

*This component requires SOC solution.*

- Create a new playbook 

- Create a webhook trigger

- Add the component as an action in the playbook

- Attach component input to the request body of the webhook 

- Add the “Write - Map Alert To Record” component from SOC solution

- Connect this to the GitHub component and map the “Alert” input to the “alert” output of the github component


Note: Traditionally, this would be configured with the webhook URL set within the github repo/org.