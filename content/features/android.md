+++
title = "Android"
description = "Every Mercurygram-specific option in the Android client: what it does, where it lives, and its default."
weight = 1

# Maintenance: this page is written by hand, in lockstep with the client. Rows
# land as options land: every Mercurygram change that adds, removes, renames,
# re-defaults or materially changes a user-facing option updates this page in
# the same unit of work. At release time only the markers below are cleared, no
# new content is written.
# Options not yet in the stable build carry a `tag-pre` span reading
# "pre-release" next to their name. To refresh the markers after a stable
# release, diff TMessagesProj/src/main/res/values/mg_strings.xml between the tag
# matching config.extra.android_version and the tip of the Mercurygram branch,
# then drop the markers on everything the tag already contains.
# Kept in the front matter, not in the body: an HTML comment there would be
# copied verbatim into the published page.
+++

Options live under **Settings → Mercurygram**, unless a section says otherwise.
They are off by default unless the Default column says otherwise, and apply to
the current account only. The ones marked *all accounts* are device-wide, which
the app also tells you in place. Options marked
<span class="tag-pre">pre-release</span> are not in the current stable build yet;
they ship in the 5-dotted pre-release builds and land in the next stable.

## Hidden accounts

The **Hidden Accounts** row appears at the top of the Mercurygram settings once
an app passcode or stealth mode makes hiding possible. A hidden account is kept
out of account switchers, settings and notifications until you type its own
4-digit unlock code, which must be unique and must not match the app passcode.
At least one account has to stay visible.

The unlock code controls in-app access only. It is not encryption: chat data,
media and credentials stay readable to anyone with full device access.

| Option | What it does | Default |
|---|---|---|
| Stealth mode | Hides hidden accounts without turning on the regular app passcode. Type a hidden account's code in the chat search field to open it for the session. | Off |
| Only show settings when using a hidden account | Keeps the Hidden Accounts screen itself out of sight unless you are signed into a hidden account. | Off |
| Change unlock code / Remove hidden account | Long-press an account in the list. Removing it makes the account visible again everywhere. | n/a |

## General

| Option | What it does | Default |
|---|---|---|
| Show "Message Details" | Adds a **Message Details** entry to the message long-press menu, including Export as JSON. | Off |
| Hide keyboard on chat scroll | Drops the keyboard as soon as the message list starts scrolling. | Off |
| Hide "All Chats" tab | Removes the All folder tab. Long press the title bar to show it temporarily. | Off |
| Default launch folder | The chat list opens on the folder you pick, on the first tab build after launch. Local to this device. | All Chats |
| Hide stories | Removes the stories bar from the chat list entirely. | Off |
| Hide Premium promo | Hides the Telegram Premium, Business and gifting rows in Settings and the Premium banners in the chat list. Unlocks nothing and does not touch sponsored messages. | Off |
| Use system font *(all accounts)* | Uses the device system typefaces instead of the bundled Roboto. | Off |
| Show character counter | Counts the characters in the message you are typing, for groups where a bot enforces a length limit. Hidden while Telegram shows its own remaining-characters counter. | Off |
| Delete for everyone by default | Pre-ticks "Delete for everyone" (and "Also delete for…" in private chats) in the delete dialog. You can still untick it. | Off |
| Save deleted & edited messages | Messages the other side deleted, your own included, stay in the chat, grayed out and non-replyable, and can be removed with the usual Delete; messages you delete yourself are not kept; edited messages keep their earlier versions under **Edit history** in the message menu. Stored separately from the Telegram cache. Self-destructing messages and secret chats are never saved. | Off |
| Clear saved message history | Wipes everything the option above recorded. Shown only while it is on. | n/a |

### Custom emoji pack

A sub-screen under General. Renders emoji from your own pack instead of the
built-in Noto set; any emoji the pack is missing falls back to the built-in one.
The pack stays on your device and is never shared.

| Option | What it does | Default |
|---|---|---|
| Use custom emoji pack *(all accounts)* | Switches emoji rendering to the imported pack. | Off |
| Import pack from file | Takes a `.zip` of emoji images, or an official Telegram APK to extract emoji from. | n/a |
| Remove pack | Deletes the imported pack and goes back to the built-in set. | n/a |

## Media

| Option | What it does | Default |
|---|---|---|
| Use rear camera for video messages | Round video messages start on the rear camera. | Off |
| Disable Live Photos by default | Sends only the still frame of a Google Motion Photo. Tapping the motion icon in the attach panel still enables it for one selection. | Off |
| Disable proximity sensor *(all accounts)* <span class="tag-pre">pre-release</span> | Keeps the screen on when the phone is near your face during calls and voice message playback, for phones whose sensor misfires. Raise-to-listen and the switch to the ear speaker stop working. | Off |

## Privacy

| Option | What it does | Default |
|---|---|---|
| Reduce network tracking *(all accounts)* | Rotates the session key every hour instead of once a day, so a passive observer has a harder time correlating your device across IP changes. Background network activity rises slightly, and the first key after a fresh login is still observable once. If the server rejects the shorter lifetime, that account falls back to the standard 24h key and the screen says which. | Off |
| Tor <span class="tag-pre">pre-release</span> *(all accounts)* | Opens the Tor screen, which is also reachable from Settings → Data and Storage → Proxy Settings and from the login screen, so an account can be logged in over Tor. Routes Telegram protocol traffic (MTProto) through an embedded Tor daemon, defeating the passive `auth_key_id` correlation that links your account to your real IP. Media downloads and other HTTP traffic stay direct. Tor stops when the app is idle and restarts on demand. Calls may suffer, and Telegram still sees the Tor exit. Needs the companion Tor plugin, which the app offers to install. While Tor is on it owns the connection: adding, picking or deleting a regular proxy is refused with a hint instead of quietly taking over, and the proxy you had before is restored when you turn Tor off. | Off |
| ↳ Anti-censorship *(all accounts)* | **Direct connection** where Tor is not blocked, **Snowflake** where it is (domain-fronted, no setup), or **obfs4 bridges** with lines from @GetBridgesBot. | Direct connection |
| ↳ Stop Tor after idle *(all accounts)* | Never, 1 minute, 5 minutes, 15 minutes or 1 hour. | 5 minutes |
| Disable global search | Search stops looking up public usernames, channels and messages across Telegram, and only covers your own chats and contacts. | Off |
| Disable AI text editor | Hides the AI button in the message and caption editors, which sends your draft to Telegram's AI service. | Off |
| Disable AI summaries | Hides the AI Summary button, which sends the message text to Telegram's AI service. | Off |
| Open links in browser | Link taps open the page in your browser instead of Instant View, which is rendered by Telegram's servers. The explicit Instant View button still works. | Off |
| Disable link previews | Stops the app fetching web page previews while composing, in every chat, so Telegram's servers never load the links you type or paste. | Off |
| Strip tracking parameters | Removes click-tracking parameters (`utm_*`, `fbclid`, `gclid`, `si` and similar) from links you open and links you paste into the message field. The rest of the address is untouched. | Off |
| Keep drafts on this device | Unsent drafts are never uploaded to Telegram, so they stop appearing on your other devices. Clearing a draft still syncs, so a draft stored before you turned this on can be removed from the server. | Off |
| Confirm Telegram links | Asks before opening `t.me` and `tg://` links and shows the address first, against links that quietly join a channel or open a bot. | Off |
| Start new chats as secret | The compose button creates an end-to-end encrypted secret chat instead of a regular one. Secret chats live only on this device. Existing chats and other ways of opening a chat are unaffected. | Off |

### Translation

A sub-screen under Privacy. Applies to all accounts.

| Option | What it does | Default |
|---|---|---|
| Translation engine | **Telegram cloud** sends the text to Telegram (which forwards to Google). **Alternative HTTP** routes it through a public [Mozhi](https://codeberg.org/aryak/mozhi) privacy proxy. **Offline** hands each translation to a separate FOSS app over a bound service, so the message never leaves the device; formatting may be lost, since the engine returns plain text. **Default** defers to Telegram's own setting. | Default (Telegram cloud) |
| Install Offline Translator from F-Droid | Opens the listing for `dev.davidv.translator`, the reference offline provider. Open it once afterwards to download your language pairs. | n/a |
| Auto-fallback on failure | If the offline translator returns nothing (no model, language not detected, service unreachable), fall back to the Alternative HTTP path. The Telegram cloud is never used as a fallback once you picked the offline engine. | **On** |
| Engine (Alternative HTTP) | DuckDuckGo, LibreTranslate, Google (via Mozhi), MyMemory or Reverso. | DuckDuckGo |
| Instance (Alternative HTTP) | Rotate across the default Mozhi instances, pin one of them, or enter a custom `https://` URL. The instance operator can log what it translates. | Auto (rotate across defaults) |

### Voice transcription

A sub-screen under Privacy. Transcribes voice and round video messages on the
device with [whisper.cpp](https://github.com/ggml-org/whisper.cpp): the audio
never leaves your phone and it works without Telegram Premium. The models are
open source (MIT) and are downloaded or imported separately, not bundled.

| Option | What it does | Default |
|---|---|---|
| Transcribe on device *(all accounts)* | Uses the local model instead of Telegram's premium-gated transcription request. Needs a model installed. | Off |
| Model *(all accounts)* | Tiny (smaller, faster), Base (larger, more accurate) or Small (most accurate, slower). | Tiny |
| Download model / Import model from file / Delete model | Fetch a model over the network, or import one you already have. | n/a |
| Language | **Automatic** lets the model detect the spoken language; **Device language** or a specific language pins it, which helps because the smaller models often mis-detect short messages. | Device language |
| Skip silence (voice detection) *(all accounts)* | Detects speech and skips the silent parts, so the model cannot invent words during silence. Uses a small extra model downloaded alongside the main one. | **On** |

## Updates

Hidden on F-Droid builds, which update through F-Droid itself. Applies to all
accounts.

| Option | What it does | Default |
|---|---|---|
| Disable in-app updater | Stops the startup check for new releases on GitHub. Manual checks still work. | Off |
| Accept pre-release updates <span class="tag-pre">pre-release</span> | Receives the 5-dotted development snapshots taken between stable releases (such as 12.6.4.4.42). They may crash or carry half-finished features; turning the option back off offers you the matching 4-dotted stable as an update, rolling the install back. Installing a pre-release any other way switches the option on by itself, so it always shows the channel you are on. | Off |
| Check for updates now | Runs the check immediately and shows when it last ran. | n/a |

## Notifications

Push runs over [UnifiedPush](https://unifiedpush.org) instead of Firebase, via
the [aesgcm-proxy](https://github.com/Mercurygram/aesgcm-proxy) gateway. Applies
to all accounts.

| Option | What it does | Default |
|---|---|---|
| Disable UnifiedPush <span class="tag-pre">pre-release</span> | Stops push notifications: the distributor subscription is dropped and both device tokens are revoked on Telegram's side. Applied immediately, no restart. Background delivery then depends on Telegram's own connection, so enable Background Connection or Keep-Alive Service under Settings → Notifications and Sounds if messages are still wanted while the app is closed. | Off |
| UnifiedPush Distributor | Picks the installed distributor app that receives pushes. Long press for recent notification and decryption statistics. | Not set |
| ↳ Google FCM (built in) | Entry in the same menu for devices with Play Services and no distributor app installed. Delivers through Firebase Cloud Messaging without bundling any Google library or Firebase project: Play Services is asked for a plain WebPush endpoint, and the gateway signs the pushes it cannot sign itself. Payloads stay end-to-end encrypted, but Google learns that a notification reached the device, so the entry is never selected automatically and warns before it is. | Not set |
| Gateway URL | The URL prefix of the UnifiedPush gateway. | `https://p2p.belloworld.it/` |

The default `ntfy.sh` server has very low rate limits and blocks the gateway, so
the app warns and switches away from it. A self-hosted ntfy server or another
distributor works fine.

## Elsewhere in the app

| Option | Where | What it does |
|---|---|---|
| OpenStreetMap map previews | Settings → Privacy and Security → Map preview provider | Renders map previews on the device with MapLibre and OpenStreetMap instead of Google. Always offered, whatever the server suggests. |
| Stickers / GIFs / Games / Inline Bots | Group permissions, and the per-member restriction editor | Splits Telegram's single "Stickers & GIFs" permission into four independent toggles. |
| Disable Secure Flags | Debug menu (long press the version number) | Allows screenshots and recents previews in screens that normally block them. |
| Remove Ads & Proxy Sponsor | Debug menu | Drops sponsored messages and the proxy sponsor channel. |
| Tor <span class="tag-pre">pre-release</span> | Settings → Data and Storage → Proxy Settings, and the proxy button on the login screen | The same Tor screen as under Settings → Mercurygram, placed where connection settings live so it can be turned on before logging in. |

## Always on

Some of the fork is not a toggle. These behaviours are always active.

### Privacy and networking

- **CDN redirects are refused.** When the server hands out a CDN redirect for a
  download, the app declines it once per file, so your permanent `auth_key_id`
  never reaches a third-party CDN. This is independent of *Reduce network
  tracking*.
- **A fresh perfect-forward-secrecy handshake on every network change**, so
  moving between Wi-Fi and mobile data does not carry the old session key over.
- **No DNS-over-HTTPS fallback to Google.**
- **No voice or round-video playback from the lock screen**, including Bluetooth
  and headset keys, and the sender's name and avatar are kept out of the
  lock-screen player. Music playback is unaffected.
- **De-googled.** MapLibre and OpenStreetMap instead of Google Maps, Noto emoji
  instead of Apple's, UnifiedPush instead of Firebase. Play Services, SafetyNet,
  Play Integrity, Cast, ML Kit and Wallet are stubbed out, passkeys are
  disabled, and BoringSSL, FFmpeg, libvpx, dav1d and tde2e are built from source.

### Premium gates removed

- Eight accounts instead of three.
- The Premium app icons.
- The per-language "Do Not Translate" list.
- Free folder reordering, including moving "All chats" off the first position.

### Interface

- The user or chat ID in Profile Info, and long-pressing a profile title copies
  the name.
- An **Administrators** entry in group and channel info.
- **Mention** in the text selection toolbar, by user ID or from your contacts.
- **Translate** in the selection toolbar of the message and caption editors,
  with "Use This Translation". Forced on-device in secret chats.
- **Remove all proxies** as a bulk action in the proxy list.
- Search that folds decorated Unicode fonts, so typing `Cucina italiana` finds
  `ℂᑌℂℐℕᗅ ℐᝨᗅℒℐᗅℕᗅ`. Applies to chat search, contact and member pickers, and the
  forward and share lists.
- The animated 🍑 emoji, restored.
- Material You / Monet dynamic themes.
- Inline `code` is always tap-to-copy, all profile photos load rather than the
  first 80, and the sticker picker shows every stored recent sticker rather than
  20.

### Media

- **Editing keeps the resolution.** The crop is cut out of the original file
  rather than out of a copy that has already been shrunk to the send size, so a
  photo cropped to a quarter of the frame is sent at the full 1280 px (or
  2560 px in high quality) instead of a quarter of it. A photo that
  also went through a filter is cut out of the filtered working copy, which the
  editor caps at 2560 px. The editor's
  working file is also saved near-losslessly, so sending no longer re-compresses
  an already-compressed image, and picking high quality on a photo sent outside
  an album now really sends it at high quality.

### Fixes carried ahead of upstream

The fork also carries upstream bug fixes: the Android 16 heads-up notification
bug, a set of crash and memory-leak fixes, secret-chat delete-for-everyone
propagation, IPv6 and multi-address proxy connectivity, several performance
fixes for large accounts, and a batch of photo picking and editing fixes (a
crop that could silently send the uncropped original, a caption lost when send
was pressed or moved onto the wrong photo when the selection was reordered,
rotating in the crop editor discarding the crop, and images pasted from Gboard
skipping the editor).
