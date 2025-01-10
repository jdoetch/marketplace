Securonix SNYPR - List All Policies component is an integration within the Securonix SNYPR security analytics platform designed to fetch all security policies configured within the system. It serves as a crucial tool for security professionals seeking to automate policy retrieval for compliance and monitoring purposes, ensuring all security measures are consistently applied and managed.

This component queries Securonix SNYPR using four required inputs to retrieve a list of incidents in the specified time period and the count of violators for each violation. A header parameter is required. The value (according to Securonix) should be:

application/vnd.snypr.app-v3.0+json

NOTE: In the component this value is filled in and can be overridden if necessary.

The required input parameters are:

type

Enter the type as list. This parameter is required.

from

Enter the start time (EPOCH) in ms. This parameter is required.

to

Enter the end time (EPOCH) in ms. This parameter is required.

rangeType

Enter any of the following range types:

updated

opened

closed

This parameter is required and must be selected in the component action.

The optional input parameters are:

offset

This parameter is optional and used for pagination.

status

Enter the status of the incident. This parameter is optional.

allowChildCases

Enter true to receive the list of child cases associated with a parent case in the response. Otherwise, enter false. This parameter is optional.

max

Enter the maximum number of records the API will display. This is a numeral value and it is optional.

sort

Enter any of the following range types:

updated

opened

closed

This parameter is required but must be selected in the component action if used.

The output is a JSON object with the results.