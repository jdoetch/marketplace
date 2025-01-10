
## Summary
This component provides a flexible way to search Jira issues. It begins by determining whether to use a provided JQL query or to build a JQL query from a search phrase and project key. Based on user input, it updates internal variables with the appropriate JQL. It then executes a search using the assembled or provided JQL and returns the resulting issues and total count.
## Actions and Their Purpose
### Search_Issues_Variables
Type: createVariables
Purpose: Initializes a variable for the JQL that will be used in the search.
On success: Calls Check_For_Search_Phrase_or_JQL.
### Check_For_Search_Phrase_or_JQL
Type: transformation
Purpose: Determines if the user provided a search phrase or a JQL query. If both are empty, it proceeds to logic that handles building a JQL.
On success: Calls parallel_ay18a.
Within this transformation:
- It checks if search_phrase is empty or not.
- It checks if jql is empty or not.
### parallel_ay18a
Type: parallelGroup
Purpose: Runs two conditional checks in parallel to decide how to form the final JQL. If the user provided a search phrase, it builds a JQL based on that phrase and project key. If the user provided a JQL directly, it updates the variable accordingly.
On success: Calls Search_Issue.
Within parallel_ay18a:
#### Check_For_Search
Type: conditional
Purpose: If the search_phrase was not empty, it takes no action. If it was empty, it triggers the Create_Search_JQL action.
#### Create_Search_JQL
Type: transformation
Purpose: Constructs a JQL using the provided search_project_key and search_phrase.
On success: Calls Update_Search_Var_With_JQL to store the generated JQL in the variable.
#### Update_Search_Var_With_JQL
Type: updateVariables
Purpose: Saves the newly formed JQL into the jql variable.
On success: Returns to parallel_ay18a’s completion.
#### Check_For_JQL
Type: conditional
Purpose: If the original jql input was not provided, it updates the jql variable with the user-provided JQL input. If no JQL was given, it uses the existing logic.
#### Update_JQL_Variable
Type: updateVariables
Purpose: Stores the provided JQL from inputs into the jql variable if no search_phrase was provided.
On success: Returns to parallel_ay18a’s completion.
### Search_Issue
Type: connector
Purpose: Executes the Jira search using the finalized jql variable and the specified maxResults.
On success: The component concludes, returning issues and total count.
## Process Flow Summary
1. The component starts by setting up a jql variable.
2. It checks if the user supplied a search_phrase or a jql directly.
3. If a search_phrase is given, it builds a custom JQL from the phrase and project key. If jql was provided, it uses that directly.
4. In parallel, it determines which JQL to use and updates the variable accordingly.
5. Once the JQL is finalized, it executes the Jira search.
6. The component finishes by returning the issues and total count resulting from the search.
If any of the conditions are not met, it defaults to logic that ensures a proper JQL is assembled or uses the user-provided JQL. This flexible structure allows the component to handle multiple input scenarios gracefully.