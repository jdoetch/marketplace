# Censys ASM - Search Risk Instances Component Documentation

## Overview
The "Censys ASM - Search Risk Instances" component is designed for security analysts who need to automate the identification and analysis of risky network instances as reported by Censys, a cybersecurity vendor. This component is essential in proactive security surveillance, as it streamlines the process to fetch and analyse Censys-identified risks within the user's infrastructure.

## Summary
This technical documentation details each action within the "Censys ASM - Search Risk Instances" component. It lays out the purpose, action type, and the conditions leading to each subsequent step such as on-success or on-failure pathways. Additionally, a comprehensive overview of the overall process flow, as triggered by this component, is provided.

## Process Flow Overview
The component operates with notably defined sequences where actions are triggered based on specified criteria related to cybersecurity assessments. After initiation, actions are processed, where if successful, they proceed along the designed workflow. Conversely, failures in actions trigger fallback or error-handling paths to ensure robustness in operations.

### Action Details

#### Error Enrichment
- **Type**: Transformation
- **Purpose**: To gather and refine information related to identified errors during data fetch operations, enhancing the detail available for risk analyses.
- **On Success**: Progresses to the subsequent enrichment actions as prescribed.
- **On Failure**: Triggers configured error handling processes to maintain operation integrity.
  
### Input Parameters
- **Error Provider**: A string identifier for the source of the error.
- **Error Result**: The outcome or result of the error encounter.
- **Error Status**: Descriptive status of the error processed.

## Pathway
Upon action initiation, the following steps are calculated:
1. Execute error enrichment
    - Upon success, proceed to detailed data transformation
    - On failure, revert to error handling procedure

## Conclusion
The "Censys ASM - Search Risk Instances" component serves as a crucial automation asset in network security management by ensuring efficient and orderly processing of risk information, facilitating timely and informed decisions in cyber defense strategies.

