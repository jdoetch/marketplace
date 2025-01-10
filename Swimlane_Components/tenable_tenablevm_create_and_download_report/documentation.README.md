# Tenable VM - Create and Download Report

## Short Description
The Tenable VM - Create and Download Report component automates the process of generating vulnerability management reports and downloading them. It is designed to streamline assessments and ensure timely accessibility to critical security insights.

## Summary of the Component
The component facilitates the creation of customized vulnerability reports based on specified templates and filters, subsequently checking report generation status, and finally downloading the report upon completion. It encompasses a sequence of defined actions aimed at maximizing the efficiency of report management within the Tenable VM framework.

### Actions and Workflow

#### 1. Create Report
- **Type**: HTTP
- **Purpose**: Initiates the creation of a vulnerability report using specific templates and filters.
- **Steps**:
  - **On-Success**: Proceed to Get Report Status
  - **On-Failure**: Handle errors accordingly
  - **Inputs**:
    - Endpoint URL with necessary parameters
    - Headers with authentication details
    - Body containing report configurations (template, name, filters)

#### 2. Get Report Status
- **Type**: HTTP
- **Purpose**: Checks the status of the report generation process.
- **Steps**:
  - **On-Success**: Move to Download Report
  - **On-Failure**: Update Failed Result
  - **Retry Until Success**: Includes conditions and timeout settings for retry
  - **Inputs**: Endpoint for status with report ID from Create Report

#### 3. Download Report
- **Type**: HTTP
- **Purpose**: Downloads the generated report.
- **Steps**:
  - **On-Success**: Update Success Result
  - **Inputs**: Specific endpoint to download the report using the report ID from Create Report

#### 4. Update Success Result
- **Type**: Update Variables
- **Purpose**: Records the successful download of the report.
  
#### 5. Update Failed Result
- **Type**: Update Variables
- **Purpose**: Logs any issues encountered during the report generation or download process.

### Overall Process Flow Summary
The process starts by creating the report with specified parameters. After triggering the report creation, the component continuously checks the status until the report is ready. Once the report generation concludes successfully, it triggers the download action. Any failure at any step is caught and logged appropriately, allowing for possible retries or failure management mechanisms.

## Technical Documentation Style
- This documentation uses a high-contrast theme suitable for dark backgrounds, ensuring excellent readability.
- Details are structured with clear headings and subheadings for easy navigation.
- Technical terms and workflow steps are explicitly defined for better understanding.

This component assists in automating the management of vulnerability reports in a secure and efficient manner, integrating seamlessly into existing Tenable VM infrastructures.

