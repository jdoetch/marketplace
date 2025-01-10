# Censys ASM - Create new Seed

## Overview

The "Censys ASM - Create new Seed" is a component designed for integration into network security frameworks, specifically crafted to enhance asset monitoring and management through the creation of new monitoring seeds in a system. This component is an essential tool for IT security administrators aiming to automate and refine their network security by ensuring that any changes or additions to their network assets are consistently tracked and analyzed.

## Summary of the Component

This component interacts with the Censys ASM platform to facilitate the creation of new seeds, which are pivotal for the detection and tracking of network assets. The creation process includes several crucial actions and decision-making points which ensure that only valid and necessary data is integrated into the Censys platform, bolstering the effectiveness of security measures taken thereafter.

### Actions

**Error Enrichment**
- **Type**: Transformation
- **Purpose**: To process error data encountered during the creation of new seeds. This action enriches the error information to provide detailed insight and assist in troubleshooting.
- **Steps**:
  - **On-Success**: Proceeds to complete the component if the enrichment and integration are successful.
  - **On-Failure**: Logs the error details and terminates the action, preventing further execution of potentially flawed processes.
  - **On-Complete**: Finalizes the action, providing a summary of outputs, either success or failure details.

### Overall Process Flow

1. **Initialization**: Begin execution of the component, starting with the preparation or collection of required data.
2. **Error Enrichment**: Transformation action where any errors encountered are enriched with additional context to provide clarity.
3. **Decision Making**: Based on the outcome of the error enrichment, decide whether to proceed with or abort the action flow.
4. **Success Processing**: If enrichment and subsequent actions succeed, finalize the seed creation process and confirm seed activation.
5. **Failure Handling**: In case of failure, log detailed error information and halt further action to prevent propagation of errors.

This flow ensures that each new seed created through the Censys ASM platform is accurate and beneficial for enhancing network visibility and security.

### Conclusion

The "Censys ASM - Create new Seed" component is instrumental in maintaining up-to-date and comprehensive visibility of network assets. It does so by ensuring that the creation of new seeds is handled efficiently, with built-in mechanisms to handle errors gracefully and provide necessary details for system enhancement and troubleshooting.

