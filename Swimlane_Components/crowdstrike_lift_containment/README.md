Use this component to lift containment for a CrowdStrike Falcon Endpoint.  The input is an array with the AID, and the output is an array of both action results and the status after it has been returned to normal.  May take up to 2 mins. If endpoint does not respond in 2 mins, the action will fail, however the contain action will queue  and apply once the endpoint comes back online.