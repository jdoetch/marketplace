# API Void - Convert URL to HTML Component Documentation

## Overview
The "API Void - Convert URL to HTML" component is designed to automate the process of converting URLs into HTML format using the API Void platform. This document provides a comprehensive overview of each action within the component, detailing their purpose, type, inputs, outputs, and possible outcomes.

## Short Description
This component is essential in scenarios where there is a need to dynamically convert URLs into HTML content, frequently used in security operations to analyze the content served at particular URLs without directly accessing them in a browser.

## Process Flow Summary
1. **Starts with an HTTP Request:** Initiate the process with an HTTP request to retrieve data from a specified URL.
2. **Data Transformation:** Transform the HTTP response data into a structured format.
3. **Data Enhancement:** Enhance the data further, if needed, to fit the operational needs.
4. **Finalize the Process:** Convert the enhanced data into an HTML file or pass it to subsequent processes.

### Detailed Actions Description
#### 1. Create Variables
- **Type:** Create Variables
- **Purpose:** Initializes necessary variables to use throughout the component.
- **On-Success:** Proceeds to make an HTTP request.
- **On-Failure:** Ends the process or handles errors.

#### 2. HTTP Request
- **Type:** HTTP
- **Purpose:** Fetches content from the specified URL, essential for the conversion process.
- **On-Success:** Passes the fetched data to create an enrichment.
- **On-Failure:** Handles the error using a normalization process.

#### 3. Create Enrichment
- **Type:** Transformation
- **Purpose:** Structurally transforms the HTTP response data for enhanced processing.
- **On-Success:** Moves to attach the transformed data to a base file.
- **On-Failure:** Process ends or redirects to error handling.

#### 4. Base to Attachment
- **Type:** Connector
- **Purpose:** Converts the base data into an attachment format, typically an HTML file.
- **On-Success:** Updates the enrichment data post conversion.
- **On-Failure:** Error handling or process termination.

#### 5. Update Enrichment
- **Type:** Update Variables
- **Purpose:** Updates the existing enrichment details post successful conversion.
- **On-Success:** Completes the process or moves to another task.
- **On-Failure:** Error handling.

#### 6. Normalize Create Error
- **Type:** Connector
- **Purpose:** Normalizes and categorizes any errors encountered during the HTTP request process.
- **On-Success:** Updates the enrichment with error details.
- **On-Failure:** End the process.

## Conclusion
This document outlines the operations of the API Void - Convert URL to HTML component which is critical in converting URLs to their HTML equivalent securely and efficiently, supporting broader security and data analysis operations.
