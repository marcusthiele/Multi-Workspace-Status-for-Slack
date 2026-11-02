# Slack Multi-Workspace Status

Set your Slack status once and apply it to every workspace you choose. If you are a member of several Slack workspaces, you no longer have to update your status in each one.

## Features

- Set the same emoji, text, and expiration in all selected workspaces at once
- Choose the target workspaces each time. Your last selection is remembered
- Clear your status with one command
- See exactly which workspace failed and why. The remaining workspaces are still updated

## Commands

| Command        | What it does                                                                                               |
| -------------- | ---------------------------------------------------------------------------------------------------------- |
| `Set Status`   | Choose workspaces, emoji, text, and expiration. Press `⌘⇧M` to manage workspaces and `⌘⇧⌫` to clear status |
| `Clear Status` | Clears your status in the workspaces you selected last, without opening a form                             |

## Setup

The extension connects to each workspace with a Slack user token that you create yourself. You need to do this once per workspace.

1. Open `Set Status` and press `⌘⇧M` to open **Manage Workspaces**, then choose **Add Workspace**.
2. Run the **Copy Manifest and Open Slack** action (`⌘⇧O`). This copies the app manifest below and opens the Slack app page.
3. In Slack, select **From a manifest**, choose your workspace, and click **Next**.
4. Switch to **JSON**, replace the content with the copied manifest, click **Next**, then **Create**.
5. Open **OAuth & Permissions**, click **Install to Workspace**, and then **Allow**.
6. Copy the **User OAuth Token** (it starts with `xoxp-`), paste it into Raycast, and submit the form.

Manifest:

```json
{
  "display_information": {
    "name": "Raycast Multi-Workspace Status",
    "description": "Sets my Slack status from Raycast."
  },
  "oauth_config": {
    "scopes": {
      "user": ["users.profile:write"]
    }
  },
  "settings": {
    "org_deploy_enabled": false,
    "socket_mode_enabled": false,
    "token_rotation_enabled": false
  }
}
```

Some workspaces only allow approved apps. If Slack shows **Request to Install** instead of **Install to Workspace**, a workspace admin has to approve your app first.

## Troubleshooting

| Message                                 | What to do                                                                         |
| --------------------------------------- | ---------------------------------------------------------------------------------- |
| `Use a User OAuth Token (xoxp-…)`       | You pasted a different token type. Copy the **User OAuth Token** from Slack        |
| `Missing the users.profile:write scope` | Add the scope under **OAuth & Permissions**, reinstall the app, and copy the token |
| `Emoji doesn't exist in this workspace` | Custom emoji must exist in every selected workspace. Pick a standard emoji instead |
| `Token was revoked` or `Token expired`  | Remove the workspace and add it again with a new token                             |

## Privacy

Tokens are stored in Raycast's encrypted local storage and are sent only to `slack.com`. The extension requests only the `users.profile:write` scope and includes no analytics. Slack doesn't offer a narrower scope, so this one also allows changes to other profile fields, but the extension only changes your status.

To disconnect a workspace, remove it in **Manage Workspaces** and then delete the app under [Your Apps](https://api.slack.com/apps).
