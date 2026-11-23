# Karis Workbench 0.2.0

Karis Workbench opens each Happy Gateway in its own Mac window. Servers have separate sign-in
cookies, so you can use several gateways at once.

Version 0.2.0 adds setup through your existing SSH profiles. It checks a server before offering
installation, reuses a compatible gateway, and can install Gateway and Happy on a fresh Debian 13
x86-64 server.

## Install on a Mac

Choose `Karis-Workbench-0.2.0-arm64-mac.zip` for Apple Silicon or
`Karis-Workbench-0.2.0-x64-mac.zip` for Intel. Unzip it, drag **Karis Workbench** into **Applications**,
and open it there.

This pilot is signed ad hoc, without an Apple Developer ID or notarization. If macOS blocks first
launch, open **System Settings → Privacy & Security → Open Anyway** for Karis Workbench. On older
macOS versions, Control-click the app and choose **Open**. A managed Mac may require its
administrator’s permission. Real Mac first-launch and Keychain checks remain part of pilot testing.

Download the ZIP through your normal browser from the public release page. If you are using Happy’s
artifact viewer, open the release link in your system browser: the native artifact viewer blocks
downloads. A direct `scp` transfer is also supported.

## Connect or set up a gateway

1. Open **File → Servers… → Via SSH**.
2. Select a literal host profile from `~/.ssh/config`, or enter an included profile’s name. Workbench
   uses the system SSH client, your configured keys, and your SSH agent. It does not copy keys.
3. Click **Inspect**. For a compatible existing gateway, click **Connect** and use your existing
   account. Workbench preserves the saved local port, certificate pin and sign-in cookies.
4. For a fresh supported server, review the required Debian packages and click **Install Gateway
   and Happy**. Workbench downloads the pinned release package, verifies it, transfers it through
   SSH, and starts the gateway. The server needs root access or sudo permission; an administrator
   password, when needed, is entered privately in the app.
5. When a new administrator needs a password, set it in Workbench. Then connect and sign in as **Admin**
   with that password. Existing accounts and passwords are reused; setup does not sign in for you.

An older recognized gateway may offer **Enable connection**. This updates its web interface for
the selected connection and adds the exact local origin. It preserves the gateway backend,
certificates, accounts and Happy data. Custom or conflicting installations are reported for
administrator attention.

The certificate fingerprint comes through authenticated SSH and is checked again against the TLS
connection. A changed saved certificate is refused until you explicitly verify and add the server
again. Unknown SSH host keys must already be verified and recorded in `known_hosts`. Passphrase-protected
keys should be available through your SSH agent or Mac Keychain.

Download and transfer progress, cancellation, and retry are shown in the setup window. A compatible
existing gateway does not trigger a package download. HTTPS connections and the advanced manual SSH
form remain available.

## Release contents

- `Karis-Workbench-0.2.0-arm64-mac.zip` — Apple Silicon app.
- `Karis-Workbench-0.2.0-x64-mac.zip` — Intel app.
- `happy-gateway-linux-x64-2026.11.23.1.tar.xz` — pinned Debian x86-64 setup payload fetched by the app.
- `happy-agent-corresponding-source-2026.11.23.1.tar.gz` — corresponding public Happy Agent source, licenses and rebuild instructions.
- Installer manifest, checksums, license texts and dependency notices.

| Asset | Bytes | SHA-256 |
|---|---:|---|
| Apple Silicon ZIP | 122,860,403 | `49b6a1cfa895db52fede9af97d8749b315b1a4303064c1f3316a8e6386606913` |
| Intel ZIP | 127,567,766 | `e11b8fca36dcf0c314a056d1c75ad976a0a4682c49599178d2055939e82f259f` |
| Linux setup payload | 387,128,112 | `fc4f7cbfe4da90e8bd7eb1fdd4f762fcb1d4e4147f0393a59d9acc7d305a0718` |
| Happy Agent source materials | 52,811,319 | `9da35f8211aed3da903b06040ee634066c195922a65167006e9941ab6dd03a2b` |

Both Mac archives passed CRC checks and preserve all 14 framework symlinks. Their app resources
are identical, contain the exact reviewed installer scripts and manifest, and were signed ad hoc
with six executable signatures checked per architecture. Desktop checks passed 198/198; focused
SSH setup, download, web-origin, actual helper/upload and setup UI checks passed 33/33, 7/7, 6/6,
5/5 and 13/13 respectively. Type, lint and format checks passed.
