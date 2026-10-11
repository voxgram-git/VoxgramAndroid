## Voxgram for Android

Voxgram is a fast, simple and free messenger. This repository contains the source code of the Voxgram Android client.

Website: [voxgram.fun](https://voxgram.fun)

### Server

The client connects to the Voxgram server:

- all data centers: `31.77.10.99:20443`
  (`TMessagesProj/jni/tgnet/ConnectionsManager.cpp`, `initDatacenters`)
- server RSA public key, fingerprint `0xc047ed25f892fc0e`
  (`TMessagesProj/jni/tgnet/Handshake.cpp`, `TMessagesProj/jni/tgnet/Datacenter.cpp`) — the same key as in
  [VoxgramDesktop](https://github.com/voxgram-git/VoxgramDesktop)

If you run your own server, replace the address and the key in those files.

### Links

- Deep-link scheme: `vg://` (for example `vg://resolve?domain=username`).
- `https://voxgram.fun/...` links are opened inside the app.
- For links from other apps (browsers, other messengers) to open directly in Voxgram on Android 12+,
  publish `Tools/voxgram.fun/.well-known/assetlinks.json` at
  `https://voxgram.fun/.well-known/assetlinks.json`. Replace the SHA-256 fingerprint in it with the
  fingerprint of the key you sign release builds with:

  ```
  keytool -list -v -keystore TMessagesProj/config/release.keystore
  ```

### Compilation Guide

**Note**: this repo contains a dummy release.keystore, google-services.json and filled variables inside BuildVars.java. Before publishing your own APKs please make sure to replace all these files with your own.

You will require Android Studio 3.4, Android NDK rev. 20 and Android SDK 8.1

1. Clone the source code: `git clone https://github.com/voxgram-git/VoxgramAndroid.git`
2. Copy your release.keystore into TMessagesProj/config
3. Fill out RELEASE_KEY_PASSWORD, RELEASE_KEY_ALIAS, RELEASE_STORE_PASSWORD in gradle.properties to access your release.keystore
4. Go to https://console.firebase.google.com/, create two android apps with application IDs fun.voxgram.messenger and fun.voxgram.messenger.beta, turn on firebase messaging and download google-services.json, which should be copied to the same folder as TMessagesProj.
5. Open the project in the Studio (note that it should be opened, NOT imported).
6. Fill out values in TMessagesProj/src/main/java/org/telegram/messenger/BuildVars.java.
7. You are ready to compile Voxgram.

### License

Voxgram for Android is based on open source code licensed under GNU GPL v. 2 or later, see [LICENSE](LICENSE).
The original copyright notices in the source files are kept as the license requires.
