# TenableVM - List Asset Vulnerabilities

## Overview
The "TenableVM - List Asset Vulnerabilities" component automates the process of listing vulnerabilities for specified assets within a network using TenableVM. This document serves as a comprehensive guide detailing the component's functionality, its actions, and overall process flow.

## Purpose
The primary objective of this component is to automate the vulnerability management process by efficiently listing vulnerabilities, which helps in enhancing the security posture and compliance by enabling timely remediation or mitigation actions.

## Component Summary
This component integrates with TenableVM to fetch and list vulnerabilities associated with specific assets. This automation plays a critical role in security and IT operations by providing a streamlined approach to vulnerability management.

### Actions Described
The component comprises several actions working collaboratively to achieve the desired outcome. Each action, its purpose, and interactions are as follows:

1. **Create Workbench Filter**
   - **Type:** Connector 
   - **Purpose:** Generates a filter to be applied on the vulnerability workbench. This serves as a preparatory step that configures the necessary parameters for fetching relevant vulnerabilities.
   - **On-Success:** Proceeds to "Create URL."

2. **Create URL**
   - **Type:** Transformation
   - **Purpose:** Constructs a URL using the filter output from "Create Workbench Filter." This URL is directed towards the vulnerabilities workbench.
   - **On-Success:** Triggers "Get Enable Workbench Vulnerabilities."

3. **Get Enable Workbench Vulnerabilities**
   - **Type:** HTTP
   - **Purpose:** Utilizes the URL constructed from the previous action to fetch vulnerabilities from TenableVM. This action interacts directly with the Tenable API to retrieve vulnerability data.
   - **On-Success:** Data handling actions or further data processing steps would be initiated.

### Process Flow
The component initiates with the creation of a workbench filter, followed by the construction of a URL tailored to query specific vulnerabilities. The final step is the API call to TenableVM using the constructed URL to fetch the vulnerabilities list. The successful execution of these steps provides structured vulnerability data pertinent to the assets under scrutiny.

### Input and Output
- **Inputs:** Require a date range and filters detailing the scope and specifics of the vulnerability assessment.
- **Outputs:** Returns a list of vulnerabilities associated with the specified assets along with a count of total assets evaluated.

### Error Handling
Each action has defined "on-failure" handlers ensuring that the component responds gracefully to any failures, thereby maintaining integrity during automation execution.

## Conclusion
The "TenableVM - List Asset Vulnerabilities" component provides a critical solution in the security management toolkit, allowing organizations to streamline their vulnerability assessment and management processes efficiently.
