# TenableVM - List Assets with Vulnerabilities: Component Documentation

## 1. Overview
The "TenableVM - List Assets with Vulnerabilities" component is a structured automation workflow that integrates with TenableVM to list assets along with their associated vulnerabilities. This component is built to aid in security management by automating the asset and vulnerability discovery process.

## 2. Component Summary
The primary goal of this component is to streamline the process of querying and retrieving detailed information about assets that have vulnerabilities, using filters and transformation actions to target specific data points. This allows security analysts to efficiently manage vulnerabilities by automating the processes involved in extracting and processing data related to vulnerabilities in various assets managed via TenableVM.

## 3. Action Details
### 3.1 Create Filter String
- **Type:** Python
- **Purpose:** Constructs a filter string from provided inputs.
- **On-success:**
  - **Add Search Type:** Proceeds to transform the filter string by appending further search criteria.
- **Inputs:** 
  - `filters`: An array specifying multiple filters to apply on asset data. Requires attributes like `filter`, `quality`, and `value`.
  
### 3.2 Add Search Type
- **Type:** Transformation
- **Purpose:** Augments the initial filter string with additional search parameters.
- **On-success:** 
  - No additional actions are set to execute following this.
- **Transformation Definitions:** 
  - **Full String:** Combines action results and additional user inputs into a finalized search string.

### 3.3 Extract Filter Count
- **Type:** Transformation
- **Purpose:** Determines the count of filters applied.
- **On-success:**
  - **Count Is Greater Than 0:** Checks if the resultant count of filters is greater than a predetermined value.
- **Transformation Definitions:** 
  - **Count:** Calculates the total number of valid filters applied based on input conditions.
  
### 3.4 Count Is Greater Than 0
- **Type:** Conditional
- **Purpose:** Validates the success of the filter application by checking if the filter count is greater than 0.
- **Condition:** 
  - Uses the result from "Extract Filter Count" to evaluate the condition.

## 4. Overall Process Flow
1. **Initialize Component:** Begin by setting up necessary input conditions such as filter types and search parameters.
2. **Create Filter String:** Build a string that encodes the filter configurations for querying the asset data.
3. **Add Search Type:** Append additional search specifications to the constructed filter string.
4. **Extract Filter Count:** Perform a check on how many filters are active after transformations.
5. **Condition Check:** If the count of filters is greater than 0, deem the filter application successful; otherwise, evaluate failure scenarios.

Each step is geared towards an optimal, condition-driven process that determines the subsequent course of action based on the data processed up to that point, aiming to effectively output a tailored list of assets pertinent to the vulnerabilities defined by the search terms and conditions.

## 5. Inputs and Schema
- **Required Inputs:**
  - `filters`: An array of objects detailing the filter conditions.
  - `search_type`: A string indicating how filters should be applied, options are "and" or "or".

**Note:** For detailed understanding and guidelines on filter configuration, please refer to the respective documentation in Workbench Filters as provided in external reference materials and API endpoints.

