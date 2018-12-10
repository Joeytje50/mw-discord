# Discord (mw-discord)
MediaWiki extension for sending notifications to a Discord webhook from MediaWiki. When a certain event occurs on your MediaWiki wiki, including new edits, they can be sent as a message to a channel on a Discord server using a webhook.

Multiple webhook URLs are supported and messages will be sent to all of them using cURL, so your web server is required to have cURL installed (for most Linux distros, installing using `sudo apt install curl` should work).

**Live demo**: https://runescape.wiki (https://discord.gg/runescapewiki)

<p align="center">
  <img src="https://i.imgur.com/tCehglJ.png" alt="Example"/>
</p>

## Requirements
- **Discord webhook URL**: This can be obtained by editing a channel on a server with the correct permissions.
- **MediaWiki 1.31+**
- **cURL**

## Installation

1. Clone this repository to your MediaWiki installation's `extensions` folder using `git clone https://github.com/jaydenkieran/mw-discord.git Discord`
2. Modify your `LocalSettings.php` file and add:

```php
// Load the extension
wfLoadExtension( 'Discord' );
// Set the webhook URL(s) (string or array)
$wgDiscordWebhookURL = [ '' ];
```

For further configuration variables, see [below](#configuration).

## Configuration
This extension can be configured using the `LocalSettings.php` file in your MediaWiki installation.

| Variable | Type | Description |
| --- | --- | --- |
| `$wgDiscordWebhookURL` | string/array | Discord webhook URLs

### Optional
| Variable | Type | Description | Default |
| --- | --- | --- | --- |
| `$wgDiscordNoBots` | bool | Do not send notifications that are triggered by a [bot account](https://www.mediawiki.org/wiki/Manual:Bots) | `true`
| `$wgDiscordNoMinor` | bool | Do not send notifications that are for [minor edits](https://meta.wikimedia.org/wiki/Help:Minor_edit) | `false`
| `$wgDiscordNoNull` | bool | Do not send notifications for [null edits](https://www.mediawiki.org/wiki/Manual:Purge#Null_edits) | `true`
| `$wgDiscordSuppressPreviews` | bool | Force previews for links in Discord messages to be suppressed | `true`
| `$wgDiscordDisabledHooks` | array | List of hooks to disable sending webhooks for (see [below](#hooks-used)) | `[]`
| `$wgDiscordDisabledNS` | array | List of namespaces to disable sending webhooks for (see [below](#hooks-used)) | `[]`

## Hooks used
- `PageContentSaveComplete` - New edits to pages and page creations
- `ArticleDeleteComplete` - Page deletions
- `ArticleUndelete` - Page restorations
- `ArticleRevisionVisibilitySet` - Revision visibility changes
- `ArticleProtectComplete` - Page protections
- `TitleMoveComplete` - Page moves
- `LocalUserCreated` - User registrations
- `BlockIpComplete` - User blocked
- `UnblockUserComplete` - User unblocked
- `UserGroupsChanged` - User rights changed
- `UploadComplete` - File was uploaded
- `FileDeleteComplete` - File revision was deleted
- `FileUndeleteComplete` - File revision was restored

## Translation
This extension can be translated through the messages in the `ì18n` folder if you're a developer. As a wiki administrator, you may find it a better option to edit the messages on-site in the MediaWiki namespace.

Any excess whitespace in text that is translated will be stripped (e.g double spaces, etc).

## License
This extension is licensed under the MIT License, [see here](LICENSE) for more information. This project is originally inspired by Szmyk's [mediawiki-discord](https://github.com/Szmyk/mediawiki-discord) project, but has been rewritten completely to be more suitable for my needs.