# Github api

- [https://docs.github.com/ko/rest/quickstart?apiVersion=2022-11-28](https://docs.github.com/ko/rest/quickstart?apiVersion=2022-11-28)

## create an organization repository

- [https://docs.github.com/ko/rest/repos/repos?apiVersion=2022-11-28#create-an-organization-repository](https://docs.github.com/ko/rest/repos/repos?apiVersion=2022-11-28#create-an-organization-repository)

```bash
gh api \
  --method POST \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  /orgs/ORG/repos \
  -f name='Hello-World' \
 -f description='This is your first repository' \
 -f homepage='https://github.com' \
 -F private=true \
 -F auto_init=true \
 -F has_issues=true \
 -F has_projects=true \
 -F has_wiki=true 
```
