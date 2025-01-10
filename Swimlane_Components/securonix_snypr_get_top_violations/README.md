The Securonix SNYPR - Get Top Violations component is an automation tool designed to integrate with the Securonix SNYPR platform to efficiently identify and summarize the most significant security violations. This component serves as a critical element within security operations, aiding organizations in rapidly addressing potential security threats to maintain system integrity and compliance.

This component queries Securonix SNYPR using four required inputs to get the top violations in the specified time period and the count of violators for each violation. The required input parameters are:

dateunit

Use days or hours as the date unit of the query

dateunitvalue

The integer value representing the date unit

offset

The integer value representing the offset from the start

max

The integer value representing the maximum number of records in the result

The output is a JSON object with the results.