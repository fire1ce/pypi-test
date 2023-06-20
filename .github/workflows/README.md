Here's how you can modify the workflow to use a Personal Access Token:

Create a Personal Access Token on GitHub with repo scope.

Go to the GitHub repository where you have the workflow file, click on Settings > Secrets > New repository secret and add the Personal Access Token as a secret (e.g., name it PERSONAL_ACCESS_TOKEN).

Modify the workflow file to use this token for pushing tags:
