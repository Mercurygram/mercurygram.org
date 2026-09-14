+++
title = "Privacy policy"
description = "What the Mercurygram apps send, to whom, and why."
+++

Mercurygram is an unofficial third-party client for the Telegram messaging
service. This page describes what the Mercurygram apps for Android and Desktop
send over the network. It applies to every distribution channel (GitHub,
F-Droid, Google Play, Flathub).

## No telemetry

The apps contain no analytics, crash reporting, advertising SDK or usage
tracking of any kind. The developer receives no data from the apps. There are
no Google Play Services, Firebase or other proprietary libraries in the apps.

## Telegram

Mercurygram talks to Telegram's servers with the same protocol as the official
apps. Everything you do in the app (messages, media, contacts, phone number,
profile, calls, location shared in a chat) goes to Telegram and is covered by
[Telegram's privacy policy](https://telegram.org/privacy). Mercurygram adds no
server of its own to that path and stores nothing about you outside your
device and your Telegram account.

Sponsored messages shown in some channels are delivered by Telegram, not by
Mercurygram, and follow Telegram's rules.

To delete your account, use Settings → Privacy and Security → Delete my
account in the app, or
[https://my.telegram.org/auth?to=delete](https://my.telegram.org/auth?to=delete).

## Push notifications (Android)

Push notifications arrive through [UnifiedPush](https://unifiedpush.org). To
make Telegram's push format deliverable, they pass through a small gateway,
`https://p2p.belloworld.it/`, run by the developer. The gateway sees the
encrypted notification payload and the push endpoint it forwards to; it cannot
decrypt the payload and forwards it without storing it. You can point the app at a
self-hosted gateway from Settings → Mercurygram.

With the built-in "Google FCM" entry selected (the default on Google Play
installs when no distributor app is present), the gateway forwards the
encrypted payload to Google's Firebase Cloud Messaging, so Google learns that a
notification was delivered to your device, and when. Google cannot read the
payload. Picking any UnifiedPush distributor app keeps Google out of the path.

## Optional features that contact other servers

Each of these is off until you enable it, and only sends what is described:

- **Message translation**: the text you ask to translate goes to the
  translation backend you pick. The offline translator sends nothing. The
  Mozhi backend sends the text to one of the public
  [Mozhi](https://codeberg.org/aryak/mozhi) instances, which relays it to the
  translation engine chosen there.
- **Voice transcription**: runs on the device. The speech model is
  downloaded once from GitHub when you enable the feature.
- **Maps**: map tiles come from [OpenFreeMap](https://openfreemap.org), which
  sees the map area you are looking at.
- **Tor**: with the Tor plugin, Telegram traffic goes through the Tor network.
- **In-app updater** (GitHub builds only): checks GitHub for new releases.
- **Links**: opening a link contacts that site, like any browser would.

## Contact

Questions about this policy: see the contact details on
[belloworld.it](https://belloworld.it) or open an issue on
[GitHub](https://github.com/Mercurygram/Mercurygram/issues).
