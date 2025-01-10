This component leverages the Enable/Disable User Account Remediation Action Interface and is compatible with SOC Solution content.  It provides users the ability to revoke all current active sessions of a user that is authenticated with Azure Entra ID.  The input is the user ID or user principal name.  The outputs is text describing if the action was successful or failed.
Required permissions

https://learn.microsoft.com/en-us/graph/api/user-revokesigninsessions?view=graph-rest-1.0&tabs=http

Permission Type: Application

Permissions: User.RevokeSessions.All