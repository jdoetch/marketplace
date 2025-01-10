The "Securonix SNYPR - Get Top Violators" is a component used within security operations to automate the process of identifying the top security rule violators, leveraging the capabilities of the Securonix SNYPR platform. This automation helps in promptly pinpointing potential security threats, thereby facilitating quick and effective decision-making. The component primarily interacts with the Securonix infrastructure to gather and process critical security data.

This component queries Securonix SNYPR using four required inputs to get the top violators in the specified time period and the risk score of each violator. The required input parameters are:

dateunit

Use days or hours as the date unit of the query

dateunitvalue

The integer value representing the date unit

offset

The integer value representing the offset from the start

max

The integer value representing the maximum number of records in the result

The output is a JSON object with the results.