This component enables forcing a password reset on the next login for a user, leveraging the Enable/Disable User Account Remediation Action Interface and compatible with SOC Solution content. It takes a user ID as input and outputs the success or failure status of the action.


Usage:

- Install the component

- Configure a JumpCloud asset with administrator privileges. Make sure to set the x_org_id field with your organization id.

- Create a playbook button in your application to force a password reset for a user and pass the user id.