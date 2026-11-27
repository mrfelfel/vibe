<p align="center">
  <img src="media/readme/vibe_logo.png" alt="Vibe" width="260">
</p>

# 🤖 Vibe — Multi-Gram for Android

**Many grams. One app.**

Vibe is a multi-account, multi-server messenger for Android built on the
Telegram MTProto stack. Keep a personal Telegram account next to accounts on
servers you run yourself, switch between them freely, and never install a
second app to do it. Familiar interface, independent accounts, no lock-in.

> 🔗 Built on **MTProto API layer 232**, on top of Telegram for Android `v13.1.1`.

<p align="center">
  <img src="media/readme/android_hero.png" alt="Vibe for Android — chats and calls" width="820">
</p>

---

## 📥 Download

Builds are published in the [Releases](https://github.com/mrfelfel/vibe/releases)
tab. One universal APK
covers all four ABIs (`armeabi-v7a`, `arm64-v8a`, `x86`, `x86_64`) and runs on
**Android 6.0+**.

It is the *unrestricted* build, the direct-download flavour rather than the
Play-Store one: no Google Play restrictions, no Firebase dependency, and push
delivered by the client's own keep-alive connection instead of a cloud service.

## ✨ Why you'll like it

- 🧩 **Multi-gram** — several accounts, on Telegram and on your own servers, all in one app.
- 🌐 **Multi-server** — each account is tied to a server, and switching is one tap.
- 🏠 **Bring your own server** — connect to infrastructure you host and fully control.
- 🔎 **Adding one takes an address** — type `host:port`, the app fetches the server's key, DC and identity itself.
- 🧠 **Familiar & comfortable** — the experience you already know, no learning curve.
- 🔒 **Private** — talk on infrastructure you trust, away from the cloud.
- 🛡️ **Censorship-resistant** — your own server stays reachable when others are blocked.
- 🆓 **Open source** — read it, audit it, build it yourself.

## 🌐 How multi-account works

Every account is tied to a server, and you choose that server when you sign in:

- **Telegram** — the official network (use your normal Telegram account)
- **OwpenGram** — the public server from the upstream project, ready to use
- **Custom** — any server you or your community runs

Add several accounts on different servers and they stay cleanly separated —
different identities, different data, one app. Separation is real, not cosmetic:
each account's cached peers, files and ids are scoped to the server they came
from, so two servers that hand out the same numeric id never bleed into each
other. Official Telegram accounts count against Telegram's own limit (3, or 5
with Premium); self-hosted ones aren't subject to that — the only ceiling is the
app's own **50 accounts in total**, across every server combined.

Remove a server and every account on it goes with it — no orphaned logins left
behind pointing at a host that no longer exists.

<p align="center">
  <img src="media/readme/android_multiserver.png" alt="Choose a server, and accounts grouped by server" width="620">
</p>

## 🔌 Connect your own server

On the **server selection screen** (shown when you log in or add a new account),
tap **➕ Add server** and type the address — `chat.example.com:2398`, or
`203.0.113.10:2398`. That is the only field you have to fill in.

The app then asks the server who it is (`/owpengram/server-info` on that same
port) and fills in the rest by itself: RSA public key, data-centre id, and the
name, description and icon the operator set. Rename it or swap the icon if you
like — those are yours to edit. Save, pick the server, log in as usual.

Everything it fetched is still editable under **Advanced** — multi-DC mode, DC
id, RSA key — for a server that doesn't answer that endpoint, or when you want
to pin the key yourself.

### 🗝️ Per-server API credentials

A server can issue its own MTProto **API ID / API Hash** pair instead of
accepting the app's built-in ones. Fill both in under **Advanced**; leave both
empty to keep using the app's own credentials.

They are a pair on purpose: a half-filled one is rejected on save, because an
`api_id` the server has no matching hash for would fail every login with
`API_ID_INVALID`. The pair is stored per server and applied to `auth.sendCode`
and passkey login for every account on that server — and editing it on a live
server updates the running connection immediately, no restart needed.

> Only `host:port` is ever taken from a link or typed in. The identity a server
> claims is fetched from that address directly, so nobody can hand you a link
> that misrepresents whose server you're about to trust.

Operators can hand out a ready-made **`owpg://addserver?host=...&port=...`**
link: opening it pops the Add server screen pre-filled with the address. By
design it carries nothing else — no key, name, DC or credentials.

Server name, description and icon refresh on their own whenever a server list is
shown, so a rebrand on the operator's side appears without you re-adding
anything. Only those cosmetics — host, port, key and DC id are never touched
after you've saved them.

Don't have a server yet? Spin one up in one command with the upstream project:
👉 [owpengram-server](https://github.com/owpengram/owpengram-server)

## 🛠️ Build (Windows)

Run the interactive build script — double-click it or run from a terminal:

```bat
build-android.bat
```

It guides you through API credentials, the keystore, SDK setup and the Gradle
build, and remembers your answers in `.owpengram-build.local.json` (gitignored).
It builds the `:TMessagesProj_AppStandalone` flavour — the unrestricted,
Firebase-free one.

**Requirements:** JDK 17+, Android SDK (compile/target API 36, build-tools
36.0.0, NDK 27.2.12479018), Git. Minimum supported device API is 23
(Android 6.0).

## 🌱 Lineage

Vibe is a rebrand of the [OwpenGram](https://github.com/owpengram) Android
client, itself built on [Telegram for Android](https://github.com/DrKLO/Telegram).
The multi-server layer, the server-info lookup and the per-server credential
handling come from that lineage; this repository carries the Vibe branding and
its own changes on top.

## 📄 License

Licensed under **GNU GPL v2 or later** — see [LICENSE](LICENSE).

---

⭐ If Vibe is useful to you, a star on this repo helps a lot.
