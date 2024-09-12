# Get JIRA User Story, Bug, or Task ID GitHub Action

This GitHub Action fetches the User Story ID associated with a given JIRA subtask, or returns the ID of a User Story, Bug, or Task, then outputs it in lowercase. This can be useful for automating workflows that require the identification of parent user stories from subtasks or handling JIRA story, bug, and task issues directly.

## Prerequisites

- You need a JIRA API token for authentication.

## Inputs

| **Input Name**   | **Description**                                                | **Required** |
| ---------------- | -------------------------------------------------------------- | ------------ |
| `issue_id`       | The JIRA issue ID (can be a Subtask, User Story, Bug, or Task) | `true`       |
| `jira_user`      | The JIRA user (email)                                          | `true`       |
| `jira_api_token` | The JIRA API token                                             | `true`       |
| `jira_base_url`  | The base URL for the JIRA instance                             | `true`       |

## Outputs

| **Output Name** | **Description**                                                                                               |
| --------------- | ------------------------------------------------------------------------------------------------------------- |
| `result_id`     | The ID of the User Story associated with the subtask, or the ID of the User Story, Bug, or Task, in lowercase |

## Example Usage

```yaml
name: Fetch JIRA User Story, Bug, or Task ID
on:
  workflow_dispatch:

jobs:
  fetch_issue_id:
    runs-on: ubuntu-latest
    steps:
      - name: Get the JIRA User Story, Bug, or Task ID
        id: get_jira_issue_id
        uses: canhbk/get-jira-user-story-id@v1.1.0
        with:
          issue_id: "JIRA-123"
          jira_user: ${{ secrets.JIRA_USER }}
          jira_api_token: ${{ secrets.JIRA_API_TOKEN }}
          jira_base_url: "https://yourcompany.atlassian.net"

      - name: Display the Result ID
        run: echo "The result ID is: ${{ steps.get_jira_issue_id.outputs.result_id }}"
```

## How It Works?

1. Input Parameters: The action takes a JIRA issue ID (subtask, story, bug, or task), JIRA credentials (user email and API token), and the JIRA base URL.
2. Fetching JIRA Issue Details: It uses the JIRA API to fetch details about the given issue ID.
3. Identifying Issue Type: Based on the issue type, the action determines whether the issue is a subtask, user story, bug, or task.
   • If it's a subtask, it fetches the parent user story ID.
   • If it's a user story, bug, or task, it uses the issue ID directly.
4. Output: The resulting ID (user story, bug, or task) is returned in lowercase as an output variable for use in subsequent steps.

## License

MIT License
