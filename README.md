# Enforce git hook
Do the following:

Add a file as detailed to the .git Folder as described here: 
https://stackoverflow.com/questions/48170832/pre-commit-hook-to-check-for-jira-issue-key

### Create file

File content:
```
#!/bin/bash
# The script below adds the branch name automatically to
# every one of your commit messages. The regular expression
# below searches for JIRA issue key's. The issue key will
# be extracted out of your branch name

REGEX_ISSUE_ID="[a-zA-Z0-9,\.\_\-]+-[0-9]+"

# Find current branch name
BRANCH_NAME=$(git symbolic-ref --short HEAD)

if [[ -z "$BRANCH_NAME" ]]; then
    echo "No branch name... "; exit 1
fi

# Extract issue id from branch name
ISSUE_ID=$(echo "$BRANCH_NAME" | grep -o -E "$REGEX_ISSUE_ID")

echo "$ISSUE_ID"': '$(cat "$1") > "$1"
```

### Make file executable
In terminal, navigate to the folder and execute the following command
````
chmod u+x commit-msg
````


Hint: Show hidden files on Mac: Command + Shift + . in Finder

