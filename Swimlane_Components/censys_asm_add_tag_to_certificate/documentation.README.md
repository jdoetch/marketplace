# Censys ASM - Add Tag to a Certificate Documentation

## Overview
The "Censys ASM - Add Tag to a Certificate" component is designed to automate the process of tagging certificates in a secure and efficient manner. This component is essential in managing certificates' lifecycle within the Censys ASM platform, ensuring that they are accurately labeled for easier tracking and management.

## Component Summary
This component facilitates the addition of a tag to a specific certificate identified within the Censys ASM system. It automates the process, reducing manual overhead and room for error while ensuring consistency in tagging practices across the database.

## Actions Description
- **Enrichment - Create Error**: This action is central to handling errors during the tagging process. It categorizes and enriches errors based on the type of failure. It involves the following steps:
  - **Transformation**: Converts incoming error data into a structured format for ease of analysis.
  - **On-Success**: Proceeds to the next step if no errors are encountered.
  - **On-Failure**: Flags the operation as unsuccessful and logs the details.
  - **On-Complete**: Concludes the operation and cleans up resources regardless of success or failure.

## Process Flow
1. **Start**: The component is triggered manually or via an automated system when a new tag needs to be added to a certificate.
2. **Error Handling**: If an error occurs during the process, the "Enrichment - Create Error" action is initiated.
   - Sub-Steps:
     - Transform the error information.
     - Check for completion.
     - Log success or failure.
3. **Completion**: Upon successful addition of the tag or handling of the error, the component completes the operation, returning the success status and any new data created during the process.

## Conclusion
The component "Censys ASM - Add Tag to a Certificate" optimizes certificate management within the Censys platform by automating the tagging process. This not only ensures high-efficiency operations but also supports rigorous compliance and security standards.

