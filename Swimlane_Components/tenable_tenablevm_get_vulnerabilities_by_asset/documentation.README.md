# TenableVM - Get Vulnerabilities by Asset

## Overview

The "TenableVM - Get Vulnerabilities by Asset" component is designed to streamline security processes by retrieving vulnerabilities associated with specified assets. This is crucial for organizations to identify, analyze, and mitigate vulnerabilities in their infrastructure efficiently.

## Component Summary

This component interacts with TenableVM to fetch vulnerabilities using predefined asset filters. By inputting specific criteria, users can narrow down the search to relevant vulnerabilities, thereby optimizing the security assessment process.

### Process Flow

1. **Initialize Output String**:  
   Start with an empty output string to concatenate filter results.

2. **Check for Filters**:
   Verify if the 'filters' key exists, and extract the filter parameters.

3. **Iterate and Construct String**:
   Loop through each filter to construct a search query string based on filter attributes.

4. **Assign to Action Outputs**:
   Assign the concatenated result string to `action_outputs` for subsequent actions.

5. **Transformation - Add Search Type**:
   Append the search type to the constructed filter string for a more refined search.

6. **Count Filter Application**:
   Count the number of filters applied and proceed based on the count.

7. **Conditional Check**:
   Evaluate if the count of applied filters exceeds a predefined threshold.

### Actions Description

- **Create Filter String**:
  - Type: Python script
  - Purpose: Constructs a URL query string using filters provided.
  - On Success: Advances to add search type.
  - On Failure: Component ends.

- **Add Search Type**:
  - Type: Transformation
  - Purpose: Appends the search type to the query string.
  - On Success: Transition to the filter count.
  - On Failure: Component ends.

- **Extract Filter Count**:
  - Type: Transformation
  - Purpose: Determines the number of filters applied.
  - On Success: Check if count is above threshold.
  - On Failure: Component ends.

- **Count is Greater Than**:
  - Type: Conditional
  - Purpose: Conditional operation to check thresholds.
  - On Success: Execute further based on condition.
  - On Failure: Ends component operation.

## Conclusion

The "TenableVM - Get Vulnerabilities by Asset" component significantly aids in automating the asset vulnerability retrieval process using TenableVM, optimizing security operations and ensuring systematic vulnerability management.

