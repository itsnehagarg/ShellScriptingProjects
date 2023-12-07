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

  ## Scenario 1:

  - List all the users of the github repo.
  - Revoke the access of a user who has left the organization.

  - Create an EC2 instance
  - SSH to the EC2 instance
  - Get the shell scripting code on EC2 machine.
  - Now configure below :
    ``
    export username="itsnehagarg"
    ``
    ``
    export token="Generate the GitHub token"
    ``
 - ./list-users.sh org-name-arg1 repo-name-arg2
 - chmod 777 list-users.sh
 - Now we need to install jq
 - Use the below command:
   `` sudo apt install jq -y
   ``
   - Now lets execute the script again
   - ./list-users.sh org-name-arg1 repo-name-arg2
   - After the running the script it will display the list of users who have access to the repo.
  
```
#!/bin/bash

# GitHub API URL
API_URL="https://api.github.com"

# GitHub username and personal access token
USERNAME=$username
TOKEN=$token

# User and Repository information
REPO_OWNER=$1
REPO_NAME=$2

# Function to make a GET request to the GitHub API
function github_api_get {
    local endpoint="$1"
    local url="${API_URL}/${endpoint}"

    # Send a GET request to the GitHub API with authentication
    curl -s -u "${USERNAME}:${TOKEN}" "$url"
}

# Function to list users with read access to the repository
function list_users_with_read_access {
    local endpoint="repos/${REPO_OWNER}/${REPO_NAME}/collaborators"

    # Fetch the list of collaborators on the repository
    collaborators="$(github_api_get "$endpoint" | jq -r '.[] | select(.permissions.pull == true) | .login')"

    # Display the list of collaborators with read access
    if [[ -z "$collaborators" ]]; then
        echo "No users with read access found for ${REPO_OWNER}/${REPO_NAME}."
    else
        echo "Users with read access to ${REPO_OWNER}/${REPO_NAME}:"
        echo "$collaborators"
    fi
}

# Main script

echo "Listing users with read access to ${REPO_OWNER}/${REPO_NAME}..."
list_users_with_read_access
```

  

  

  

  




