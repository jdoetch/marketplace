# API Void - DNS Lookup Component Documentation

## Overview

API Void - DNS Lookup is designed to assist in automation and security processes by providing DNS lookup capabilities. This document details the functionality of the API Void - DNS Lookup component, explains its various actions, and offers a comprehensive process flow.

## Component Summary

API Void - DNS Lookup facilitates querying DNS to gather intelligence about domain names. This component involves several critical actions such as creating variables, updating enrichments, and handling error normalization to ensure streamlined operations across various stages of DNS lookup.

## Actions Detailed Description

### Create Variables
- **Type:** `createVariables`
- **Description:** Initializes variables for DNS lookup.
- **On Success:** Proceeds to send a HTTP request.
- **On Failure:** [Not specified]
- **On Complete:** [Not specified]
- **Inputs:** Host and action details.

### HTTP Request
- **Type:** `HTTP`
- **Description:** Executes an external API call to APIVoid to perform DNS lookup.
- **On Success:** Triggers the transformation process `Create Enrichment`.
- **On Failure:** Executes `Normalize Create Error`.
- **Inputs:** Contains the endpoint and other query parameters required for the DNS lookup.
- **Settings:** Follow redirects, verify certificates, and do not allow unsafe legacy renegotiation.

### Create Enrichment
- **Type:** `transformation`
- **Description:** Manages data transformation based on the response from the API call.
- **On Success:** Updates the enrichment with the new data.
- **On Failure:** [Not specified]
- **On Complete:** [Not specified]

### Update Enrichment
- **Type:** `updateVariables`
- **Description:** Updates variables with the transformed data for further use.
- **On Success:** [Not specified]
- **On Failure:** [Not specified]
- **On Complete:** [Not specified]

### Normalize Create Error
- **Type:** `connector`
- **Description:** Normalizes error messages received during the HTTP request process.
- **On Success:** Updates enrichment with error details.
- **On Failure:** [Not specified]
- **On Complete:** [Not specified]

## Overall Process Flow Summary
1. **Initialization:** Variables are created to hold necessary data.
2. **Execution of HTTP Request:** DNS lookup is performed using APIVoid. Depending on the outcome:
   - **Successful Response:** Proceed with data transformation.
   - **Error Response:** Normalize the error.
3. **Data Transformation:** Enrich the input with additional information from the DNS lookup.
4. **Update of Enrichment:** Enhanced data is saved or updated for downstream use.
5. **Normalization of Errors:** Standardize error format for consistency across processes.

This flow ensures that each step is handled precisely, with mechanisms for both success and error management to adapt to dynamic response scenarios from external DNS lookups.

