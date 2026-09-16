+++
title = "Desktop"
description = "Every Mercurygram-specific option in the Desktop client: what it does, where it lives, and its default."
weight = 2

# Maintenance: this page is written by hand, in lockstep with the client. Rows
# land as options land: every mdesktop change that adds, removes, renames,
# re-defaults or materially changes a user-facing option updates this page in
# the same unit of work. At release time only the markers below are cleared, no
# new content is written.
# The fork is a linear rebase, so `git log <upstream-tag>..dev` in the mdesktop
# repo is the feature list, and the option labels and defaults come from
# Telegram/SourceFiles/core/mg_settings.cpp and settings_mercurygram.cpp.
# Options not yet in the stable build carry a `tag-pre` span reading
# "pre-release" next to their name. To refresh the markers after a release,
# compare the `dev` tip against the release/X.Y.Z branch matching
# config.extra.desktop_version and drop the markers on everything that branch
# already contains.
# Kept in the front matter, not in the body: an HTML comment there would be
# copied verbatim into the published page.
+++

The Desktop client is a fork of Telegram Desktop, a different codebase from the
[Android client](@/features/android.md) and with a smaller set of options.
Everything below lives under **Settings → Mercurygram** unless a section says
otherwise, and is off by default unless the Default column says otherwise.
Options marked <span class="tag-pre">pre-release</span> are not in the current
stable build yet.

## Secret chats

Upstream Telegram Desktop has no secret chats at all: the end-to-end encrypted
chats that the mobile apps offer have never been implemented there. Mercurygram
Desktop adds them, so a secret chat started on your phone is reachable from the
computer.

Start one from **Start secret chat** in a contact's menu. The chat waits until
the other side comes online to complete the key exchange, then behaves like the
mobile one: an **Encryption key** fingerprint you can compare out of band, an
optional self-destruct timer, and deletion that can cover both sides.

This is **work in progress**. The encryption core is covered by tests, but the
feature is not yet at the polish level of the rest of the app; treat it as
usable rather than finished, and keep the phone as the reference client.

## General

| Option | What it does | Default |
|---|---|---|
| Show IDs in profile | Adds the user or chat ID to Profile Info. | Off |
| Hide stories | Removes the stories bar from the chat list entirely. | Off |
| Delete for everyone by default | Pre-ticks "Delete for everyone" in the delete dialog. You can still untick it. | Off |
| Message details menu | Adds a **Message details** entry to the message right-click menu, showing the message and peer IDs, the date and the author. | Off |
| Hide "All" folder tab | Removes the All folder tab from the folder strip. | Off |
| Hide Premium promo | Hides the Telegram Premium, Stars, TON, Business and gift rows in Settings. Unlocks nothing and does not touch sponsored messages. | Off |
| Launch folder | The chat list opens on the folder you pick. A folder that no longer exists falls back to the default. | Default folder |

## Media

| Option | What it does | Default |
|---|---|---|
| Show all recent stickers | Lifts the 20-entry cap on the recent stickers row, showing every recent sticker the app has stored. | Off |
| Send large photos | Uploads photos at up to 2560px instead of 1280px. | Off |

## Privacy

Opt-in mitigations that keep queries and drafts off Telegram's servers.

| Option | What it does | Default |
|---|---|---|
| Disable global search | Search stops looking up public usernames, channels and messages across Telegram, and only covers your own chats and contacts. In-chat search is unaffected. | Off |
| Disable link previews | Stops the app fetching web page previews while composing, and marks outgoing messages so the server generates none either, so Telegram's servers never load the links you type or paste. Previews on messages you receive are unaffected. | Off |
| Disable AI text editor | Hides the AI button in the compose field, and disables its shortcut, so your draft is never sent to Telegram's AI service. | Off |
| Disable AI summaries | Hides the AI Summary button on incoming messages, so their text is never sent to Telegram's AI service. | Off |
| Open links in browser | Link clicks open the page in your browser instead of Instant View, which is rendered by Telegram's servers. The explicit Instant View button still works. | Off |
| Reduce network tracking <span class="tag-pre">pre-release</span> | Rotates the session key every hour instead of once a day, so a passive observer has a harder time correlating your device across IP changes. Background network activity rises slightly, and the first key after a fresh login is still observable once. If the server refuses the shorter lifetime, it steps up to six and then twenty-four hours, and the note under this section says which. | Off |
| Strip tracking parameters <span class="tag-pre">pre-release</span> | Removes click-tracking parameters (`utm_*`, `fbclid`, `gclid`, `igsh` and about seventy more) from links you open, links you copy out of a message, and links you paste into the message field. Site-specific ones go too, where they are only tracking on their own site: `si` on YouTube and Spotify, `s`/`t` on X, the share ids on TikTok and Instagram's `stkn`, `ref`/`pd_rd_*` on Amazon, `ved` on Google Search. Parameters that carry real meaning are kept, such as Instagram's `img_index`. The rest of the address is untouched. A paste that carried tracking is inserted as plain text. | Off |
| Keep drafts on this device <span class="tag-pre">pre-release</span> | Unsent drafts are never uploaded to Telegram, so they stop appearing on your other devices. Clearing a draft still syncs, so a draft stored before you turned this on can be removed from the server. | Off |
| Confirm Telegram links <span class="tag-pre">pre-release</span> | Asks before opening `t.me` and `tg://` links and shows the address first, against links that quietly join a channel or open a bot. Ctrl-click skips the question, as it does for external links. | Off |

## Elsewhere in the app

| Option | Where | What it does |
|---|---|---|
| Lock when window is closed or minimized | Settings → Privacy and Security → Local passcode | Locks the app as soon as the last window goes to the tray or is minimized, instead of waiting for the auto-lock timer. Needs a local passcode. |
| Remove sponsored messages | Settings → Advanced → Experimental settings, under **Mercurygram** | Hides sponsored messages in channels. Kept behind Experimental on purpose: Telegram's API terms ask clients not to interfere with them, so it is yours to enable at your own discretion. Restarts the app. |
| Mercurygram folder <span class="tag-pre">pre-release</span> | Settings → Folders, on the create and edit screens | A switch that keeps the folder off Telegram's folder API, so it counts against neither the folder limit nor the chats-per-folder limit. Mercurygram folders carry a "Mercurygram" tag in the folder list and are synced between your Mercurygram apps through one JSON document in Saved Messages, the same one the Android client reads, so Telegram learns nothing it did not already know. |

## Always on

Some of the fork is not a toggle. These behaviours are always active.

### Privacy and networking

- **CDN redirects are refused.** When the server hands out a CDN redirect for a
  download, the app declines it once per file, so your permanent `auth_key_id`
  never reaches a third-party CDN. If the datacenter insists, the download goes
  through the CDN rather than failing. <span class="tag-pre">pre-release</span>
- **No DNS-over-HTTPS fallback to Google.** Neither the config fallback nor the
  proxy hostname resolver asks `dns.google.com`, directly or through the
  google.com domains upstream fronts it behind. Cloudflare and the Firestore
  fallback still cover both.
  <span class="tag-pre">pre-release</span>

### Premium gates removed

- Eight accounts instead of three.
- Free folder reordering, including moving "All chats" off the first position.
- The *Translate Entire Chats* switch under Settings → Language, so the in-chat
  "Translate to X" bar can always be switched off, and the per-language
  "Do Not Translate" list next to it.
  <span class="tag-pre">pre-release</span>

### Interface

- **Stickers / GIFs / Games / Inline bots** are four independent group
  permissions instead of Telegram's single bundled "Stickers & GIFs" toggle,
  both in the group defaults and in the per-member restriction editor.
- Clicking a mention opens the profile even when the app has never been told who
  that user is, for instance in a message restored from the local cache.
- Search that folds decorated Unicode fonts, so typing `Cucina italiana` finds
  `ℂᑌℂℐℕᗅ ℐᝨᗅℒℐᗅℕᗅ`. Applies to the chat list, forum topics, contact and member
  pickers, and the forward and share lists. The name as it was written keeps
  matching itself, so a chat named in Cyrillic, Greek or CJK is unaffected.
- The animated 🍑 emoji, restored.

## Builds and updates

Windows, macOS and Linux builds come from
[GitHub Releases](https://github.com/Mercurygram/mdesktop/releases),
including **arm64 builds for Windows and Linux** that upstream does not ship, and
Linux also has a [Flathub](https://flathub.org/apps/it.belloworld.mercurygram)
package and a Fedora Copr build against the distribution's own libraries.

Because this is an unofficial fork, the builds are signed with Mercurygram's own
update keys and the in-app updater points at the Mercurygram release server, not
Telegram's. The Telegram API credentials are supplied at build time and are never
committed, so anyone building from source uses their own.

## Fixes carried ahead of upstream

The fork also carries fixes that are not Mercurygram features: collapsed
community members no longer show up twice in folders that match by chat type, a
use-after-free when leaving the admin log with the back button, a build failure
on aarch64 in the chat exporter, a workaround for the webkitgtk renderer
crash that took out every in-app webview (bot mini apps, payments, Instant View,
web login) on some Linux graphics setups, and second-level context menus
(Formatting, Spelling) ignoring mouse clicks on Windows
<span class="tag-pre">pre-release</span>.
