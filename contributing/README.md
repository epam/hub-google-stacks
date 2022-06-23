# How to contribute into google-stacks repo from Cloud Shell

1. [Creating a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). Minimum required scopes are `repo`, `read:org`, `workflow`. Save this generated personal token in safe place (you can use it for future cloud shell sessions)

2. Login to github with `gh` tool using a generated personal token:

   ```bash
   gh auth login -h github.com
   ```

   `gh` tool will ask you to select some options. Select next one:

   ```text
   ? What is your preferred protocol for Git operations? HTTPS
   ? Authenticate Git with your GitHub credentials? Yes
   ? How would you like to authenticate GitHub CLI? Paste an authentication token
   ```

   Use `gh` tool as git credentials helper

   ```bash
   gh auth setup-git
   ```

3. Configure git client

   Set git user name and email manually

   ```bash
   git config --global user.name "<your_user_name>"
   git config --global user.email "<your_user_email>"
   ```

   or use your Github user name and email as `<your_github_username>@users.noreply.github.com`

   ```bash
   git config --global user.name "$(gh api https://api.github.com/user | jq -crM '.login')"
   git config --global user.email "$(echo "$(git config --global user.name)@users.noreply.github.com")"
   ```

   or use your current GCP user name and email

   ```bash
   git config --global user.email "$(gcloud auth list --verbosity=none --filter=status:ACTIVE --format="json(account)" | jq -cMr '. | first | . account')"
   git config --global user.name "$(echo "${USER/_/ }" | sed -e 's/^./\U&/g;  s/ ./\U&/g')"
   ```

4. Before making changes create git branch

   ```bash
   git checkout -b <your_branch_name>
   ```

   Make your changes and commit them

   ```bash
   git add -A .
   git commit -m "<your_commit_message>"
   ```

5. Create Github Pull Request

   ```bash
   gh pr create --title "<your_pr_title>" --body "<your_pr_description>"
   ```

   `gh` tool will ask you a question `Where should we push the '<your_branch_name>' branch?` select `Create a fork of agilestacks/google-stacks`.
   Calling `gh pr create` will create a fork repo in your Github account, push your branch changes and create a PR in `agilestacks/google-stacks`.
