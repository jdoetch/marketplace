# Maltiverse - Lookup IP Component Documentation

## Overview

The "Maltiverse - Lookup IP" component is designed for use in security operations to enhance the analysis and investigation of IP addresses by querying the Maltiverse database. This component assists security analysts by performing reputation lookups to efficiently identify potentially malicious IP addresses.

## Summary of the Component

The "Maltiverse - Lookup IP" component automates the process of IP address verification, focusing on gathering and analyzing reputation data. It integrates these functionalities into workflows to help automate and expedite decision-making in network security management.

## Actions

### Enrichment - Create Error
- **Type**: Transformation
- **Purpose**: This action serves to transform input data related to an IP error lookup into a structured error enrichment format.
- **Steps**:
  - **On Success**: Proceeds to the next step in the component upon successful transformation.
  - **On Failure**: Halts the component or transitions to error handling routines.
  - **On Complete**: Finalizes any post-transformation requirements.

#### Details of Transformations:
- **Title**: Error Enrichment
- **Inputs**:
  - **Enrichment Provider**: Source of the enrichment data.
  - **Error Provider**: Source identifier for the error data.
  - **Enrichment Type**: Defines the type of enrichment, typically set as 'reputation'.
  - **Enrichment Verdict**: Final decision of the enrichment process, labeled as 'error' in unsuccessful cases.

## Process Flow Summary

1. **Start**: The component initiates when triggered by specific conditions or manually.
2. **Perform Error Enrichment Creation**: 
   - Input data from previous operations or defined by the user is transformed into an ‘error enrichment’ format.
   - Checks the reputation of an IP and categorizes it based on predefined criteria.
3. **Decision Making**:
   - Depending on the success or failure of the enrichment process, the flow either advances or stops with appropriate actions.
4. **End**: The process concludes after finalizing the output or handling errors.

This component workflow automates critical tasks within IP address management and enhances network security protocols by allowing rapid decision-making based on reputable data.

