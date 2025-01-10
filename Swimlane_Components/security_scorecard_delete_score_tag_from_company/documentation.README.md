# SSC - Delete Scoretag from Company

## Introduction

The SSC - Delete Scoretag from Company is a critical component designed to streamline the process of managing scoring tags associated with companies in a database. This documentation outlines the detailed operations of the component, its configuration, and its interaction with a system to ensure efficient management of scoretags.

## Overview

The component enables automated removal of scoretags from company profiles, ensuring data accuracy and relevance in scoring algorithms. This component interacts with the company's systems to synchronize data across platforms effectively.

## Process and Actions

### Action: Delete Scoretag

- **Type**: Transformation
- **Purpose**: To remove a specified scoretag from a company's profile.
- **Description**: This action searches for and deletes the scoretag associated with a given company ID.

#### Subsequent Steps

- **On-Success**:
  - The system verifies that the scoretag has been successfully deleted.
  - A confirmation log is generated.
- **On-Failure**:
  - The system logs the failure.
  - An error is displayed to the user or sent to an error handling service.
- **On-Complete**:
  - The system performs a clean-up operation to close any open resources or sessions.

## Overall Process Flow

1. **Initialization**: The component is triggered through a user action or automated system process.
2. **Validation**: The system checks if the specified scoretag exists for the company.
3. **Execution**: If validation passes, the delete operation is performed.
4. **Post-Execution**:
   - On success, follow the success steps outlined above.
   - On failure, follow the failure steps as mentioned.

This streamlined process ensures that company profiles remain up-to-date by effectively managing scoretags.

## Conclusion

The SSC - Delete Scoretag from Company component plays a vital role in maintaining the integrity and relevance of company data within scoring systems. This document provides all the necessary details to understand and implement the component effectively.

