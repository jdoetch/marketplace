# Criminal IP - Get Domain Reports Component Documentation

## Overview

The "Criminal IP - Get Domain Reports" component is designed to automate the retrieval of domain reputation reports from the Criminal IP database. This component assists cybersecurity efforts by collecting and normalizing data related to domain reputations, which can be crucial for threat intelligence and incident response processes.

## Purpose

The primary reason for this automation flow is to streamline the process of fetching and analyzing reputation data from Criminal IP, a vendor known for providing comprehensive insights into domains potentially involved in cybercriminal activities. This component enhances security measures by allowing automated checks against domains, thereby identifying malicious activities promptly.

## Action Summary

1. **Create Variables**: Initializes necessary variables for processing.
   - **Type**: Variable Creation
   - **Purpose**: Sets up the required data structures for domain reports retrieval.
   - **On-Success**: Proceed to request domain data.
   - **On-Failure**: None specified.
   
2. **HTTP Request**: Executes a request to the Criminal IP API to fetch domain reports.
   - **Type**: HTTP
   - **Purpose**: Gathers domain data from the Criminal IP API.
   - **On-Success**: Pass data to "Create Enrichment".
   - **On-Failure**: Executes "Normalize Create Error Action".

3. **Create Enrichment**: Transforms the fetched data into a structured format.
   - **Type**: Transformation
   - **Purpose**: Structures raw API data into a more usable format.
   - **On-Success**: Proceed to update enrichment data.
   - **On-Failure**: None specified.

4. **Update Enrichment**: Updates the enrichment data with new information.
   - **Type**: Variable Update
   - **Purpose**: Refreshes the stored enrichment data with new insights.
   - **On-Success**: None specified.
   - **On-Failure**: None specified.

5. **Normalize Create Error Action**: Handles HTTP errors or data fetching issues.
   - **Type**: Error Handling Connector
   - **Purpose**: Manages errors during data fetching, ensuring stability.
   - **On-Success**: Proceed to update enrichment.
   - **On-Failure**: None specified.

## Overall Process Flow

The component begins by initializing necessary data structures, followed by an HTTP request to the Criminal IP API to fetch domain reports. If the request succeeds, the data is passed to the "Create Enrichment" action, which structures the data accordingly. This structured data is then updated using the "Update Enrichment" action. In case of any failure during the HTTP request, the "Normalize Create Error Action" manages the error and the flow proceeds to update the enrichment data, ensuring the component recovers gracefully from errors.

Concluding the flow, the overall component ensures that domain data is not only retrieved but also structured and integrated into the wider system efficiently, supporting enhanced security operations.

