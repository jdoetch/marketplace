# Censys - Delete Tag Component Documentation

## Overview
This document serves as the detailed technical documentation for the "Censys - Delete Tag" component. The component is designed to facilitate the deletion of tags from assets in the Censys database via an integrated system. It helps maintain the accuracy and relevance of tag-based categorization within Censys, ensuring data integrity and operational efficiency.

## Purpose
The existence of this component is critical for maintaining clean and accurate tags on assets within Censys. By automating the deletion of tags, it minimizes human error, streamlines processes, and enhances security protocols.

## Process Flow Summary
The component operates through a sequence of steps initiating with a variable creation, making an HTTP request, and based on the response, either updates the enrichment or handles error normalization. All actions are carried out with provision for success and failure paths ensuring robustness in tag management operations.

### Action: Create Variables
- **Type**: Create Variables
- **Description**: Initializes necessary variables for the process.
- **On Success**: Makes an HTTP request.
- **On Failure**: Not specified.

### Action: HTTP Request
- **Type**: HTTP
- **Description**: Sends an HTTP request to the Censys API to delete a specified tag.
- **Endpoint**: Constructed dynamically using tag data.
- **On Success**: Proceeds to Create Enrichment.
- **On Failure**: Executes Normalize Create Error ATWC.

### Action: Create Enrichment
- **Type**: Transformation
- **Description**: Handles the data transformation post successful HTTP request.
- **On Success**: Updates Enrichment based on transformation data.
- **On Failure**: Not specified.

### Action: Normalize Create Error ATWC
- **Type**: Connector
- **Description**: Normalizes error data from the HTTP request process.
- **On Success**: Updates Enrichment with error normalization.
- **On Failure**: Not specified.

### Action: Update Enrichment
- **Type**: Update Variables
- **Description**: Updates enrichment variables post creation or error handling.
- **Input**: Based on results from previous actions (Create Enrichment or Normalize Create Error ATWC).
- **On Success**: Concludes the action chain.
- **On Failure**: Not specified.

## Final Note
This component ensures efficient tag management within Censys, providing automated, reliable, and error-handled operations to maintain the integrity and relevance of asset tagging.

