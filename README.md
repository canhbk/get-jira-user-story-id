# Get JIRA User Story ID GitHub Action

This GitHub Action fetches the User Story ID associated with a given JIRA subtask or user story ID, then outputs it in lowercase. This can be useful for automating workflows that require the identification of parent user stories from subtasks or handling JIRA story issues directly.

## Prerequisites

- You need a JIRA API token for authentication.

## Inputs

| **Input Name**   | **Description**                                     | **Required** |
| ---------------- | --------------------------------------------------- | ------------ |
| `issue_id`       | The JIRA issue ID (must be a Subtask or User Story) | `true`       |
| `jira_user`      | The JIRA user (email)                               | `true`       |
| `jira_api_token` | The JIRA API token                                  | `true`       |
| `jira_base_url`  | The base URL for the JIRA instance                  | `true`       |

## Outputs

| **Output Name** | **Description**                                                    |
| --------------- | ------------------------------------------------------------------ |
| `user_story_id` | The ID of the User Story associated with the subtask, in lowercase |

## Example Usage

```yaml
name: Fetch JIRA User Story ID
on:
  workflow_dispatch:

jobs:
  fetch_story_id:
    runs-on: ubuntu-latest
    steps:
      - name: Get the JIRA User Story ID
        uses: canhbk/get-jira-user-story-id@v1.0.0
        with:
          issue_id: "JIRA-123"
          jira_user: ${{ secrets.JIRA_USER }}
          jira_api_token: ${{ secrets.JIRA_API_TOKEN }}
          jira_base_url: "https://yourcompany.atlassian.net"

      - name: Display the User Story ID
        run: echo "The user story ID is: ${{ steps.get_jira_user_id.outputs.user_story_id }}"
```

## How It Works?

1. Input Parameters: The action takes a JIRA issue ID (subtask or story), JIRA credentials (user email and API token), and the JIRA base URL.
2. Fetching JIRA Issue Details: It uses the JIRA API to fetch details about the given issue ID.
3. Identifying Story or Subtask: Based on the issue type, the action determines whether the issue is a subtask or user story.
   • If it’s a subtask, it fetches the parent user story ID.
   • If it’s a user story, it uses the issue ID directly.
4. Output: The user story ID is returned in lowercase as an output variable for use in subsequent steps.

## License

MIT License
