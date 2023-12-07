# Shell Scripting Project-1

## GitHub API integration module 

We will talk to Github API to get more information about the application. Developers can make API calls to get more info about the application they are looking for.

Info that we are planning to retrieve from GitHub in this script can include:

- No. of repos
- passwords
- No. of issues
- No. of projects
- Who are the collaborators on a repo/ Who have access to a repository?

  This script can also be used as an module. Module means other devops engineers can also use this script to get information. lets say a Team was trying to integrate JIRA integration with GitHub, bugzilla and a reporting dashboard.

  Let's use the below link to understand more about the REST APIs for GitHub Pull requests:

  https://docs.github.com/en/rest/pulls/pulls?apiVersion=2022-11-28

```
  curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/pulls
```
  In the above curl command replace OWNER and REPO values with your owner and repo.

  

  

  

  

  




