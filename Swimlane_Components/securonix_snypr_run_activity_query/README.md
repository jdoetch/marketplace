The Securonix SNYPR - Run Activity Query component is crafted to automate and streamline the extraction and analysis of activity data within security frameworks using the Securonix platform. This technical utility enhances operational efficiencies by allowing detailed and targeted searches of activity logs, critical for timely threat detection and response. It functions as a key element in maintaining vigilant and responsive security measures.

This component is used to query the Securonix SNYPR event data and return a response. Activity, also known as "event data", are security logs collected from a variety of structured and unstructured data sources by Securonix. These logs are enriched at time of ingestion with identity, threat intel, and other sources of context. The input is a query in the form of:

 index=activity AND resourcegroupname = <datasourcename> AND <additional conditions>

Two parameters are also required as inputs: 

eventtime_from 

eventtime_to

Best practice is to search for no more than seven days (according to Securonix). 

Important Note: Time must be in the format of:  MM/dd/yyyy HH:mm:ss

Optional input parameters include the following:

tz

Enter the timezone. If empty, the application timezone will be selected. This parameter is optional.

prettyJson

Enter true or false. If set to true, sends the REST response in a pretty JSON format else raw format. By default, it is set to False. This parameter is optional.

max

Enter the number of records you want the REST API to return. Default is 1,000 and Max is 10,000. This parameter is optional.

queryId

Used for paginating through the results in the specified duration to get the next set of maximum records. When you run the query for the first time, the response has queryId. You can use the query ID to look for records on a specific page.

The output is a JSON object with the results.