This component ingests alerts from Microsoft Defender for Endpoint as Case and Incident Management records, creates Threat Intelligence records for any observables, and relates those TI records to their corresponding CIM record.

**Usage:**

- Install the component

- Configure a Microsoft Defender Asset

- Create a playbook to ingest from Microsoft Defender EDR, or using an existing playbook

- Configure the Component’s input parameters:

    - Ingest From Timestamp: Required. Can be created using a transform block to get current time, then subtract X minutes from current time

    - Signal Source: Required. Ensure that your Application has a Signal Source field with a value defined for Microsoft Defender

    - Organization: Optional

**Inputs:**

- Ingest From Timestamp:

    - key: Ingest_From_Timestamp

    - Required

    - This input is the timestamp you’d like to ingest from when pulling alerts from MS Defender EDR

- Signal Source

    - key: Signal_Source

    - Required

    - Depending on how the user has configured the signal source field in their application, this could be different. So instead of hardcoding it to a specific value (e.g. Microsoft Defender EDR), the user can input how they want to specify the signal source

- Organization

    - key: Organization

    - Not Required

    - This is an optional field that may be included in the created alert records

**Outputs:**

- Aggregated_Case_Create_Fields_List

    - This output is a list of objects. Each object contains common fields specified used to create a standard Case and Incident Management record. It’s an aggregated list of two different types of objects: Case Create Fields With Observables and Case Create Fields No Observables. This depends on whether an alert contains any Evidence/Observables.