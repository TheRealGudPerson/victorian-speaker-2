# Victorian Speaker

A Revenge plugin for Android Discord that rewrites outgoing messages into playful Victorian-style English.

## Three styles

- **Tea & Toast** — light touch: “thanks” becomes “many thanks”.
- **Drawing Room** — moderate formality: “hello” becomes “I bid you good day”.
- **Royal Decree** — deliberately extravagant: “please” becomes “I beseech thee”.

Choose the active style using the three compact buttons added to the chat composer action row. The selected style is saved locally.

## Behaviour

- Rewrites message text immediately before Discord sends it.
- Leaves URLs, inline code, and fenced code blocks unchanged.
- Preserves other message fields, including attachment metadata.
- Does not edit the visible draft while typing.
- Runs entirely on-device. No message text is sent to an external rewriting service.

The first version uses a local phrase dictionary, not a language model. This keeps it private and fast, but it will not perfectly rewrite arbitrary sentences.

## Install in Revenge

**Repository URL:**

`https://therealgudperson.github.io/victorian-speaker-2/index.json`

1. Make sure you are using the Revenge Android client.
2. Open **Settings → Revenge → Plugins**.
3. Tap the settings gear beside the Plugins heading.
4. Add the repository URL above. Revenge should fetch its index.
5. Open the plugin browser, find **Victorian Speaker**, and tap **Install**.
6. Return to the plugin list and enable **Victorian Speaker**.

If the repository cannot be reached, check that GitHub Pages is enabled for this repository (see **First-time publishing** below).

### Install from a ZIP instead

You can also sideload the plugin without adding a repository:

1. Open the [latest successful build](https://github.com/TheRealGudPerson/victorian-speaker-2/actions/workflows/build.yml).
2. Open the successful workflow run and download the `Victorian-Speaker-Android-Plugin` artifact.
3. Extract the downloaded artifact. Inside is `Victorian-Speaker-install.zip`.
4. In Revenge, open **Settings → Revenge → Plugins**, tap the settings gear, and choose **Install from file**.
5. Select `Victorian-Speaker-install.zip`, confirm the installation, and enable the plugin.

ZIP installs are sideloaded and do not receive repository-based automatic updates.

## First-time publishing

The build workflow automatically creates the installable ZIP and publishes `index.json` plus the versioned ZIP to the `gh-pages` branch.

After the first successful workflow run:

1. Open this repository's **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select **gh-pages** as the branch and **/(root)** as the folder, then save.
4. Wait for GitHub Pages to finish deploying. The repository URL above should then return the plugin index.

## Build locally

This repository uses the official Revenge plugin CLI.

```sh
bun install
bun run build victorian-speaker
```

The JavaScript bundle is written to `plugins/victorian-speaker/build/js/index.js`.

## Compatibility and testing

The plugin targets the Revenge API range declared in `manifest.json`. It hooks the outgoing `sendMessage` action and the `ChatInputRightActions` composer component.

A successful CI build confirms that the code bundles and packages. It does not prove that Discord's internal composer component is identical on every Android client version. After installing, verify that the three mode buttons appear and that a test message is transformed before relying on it.

## Privacy and permissions

All rewriting happens locally on the device. The plugin does not send message content to a third-party service. Plugins run inside the Discord client, so only install it if you trust the source.

## Ideas for later versions

- Preview the transformed message before sending.
- Add a custom phrase dictionary and user-defined substitutions.
- Add per-server or per-channel default styles.
- Add a one-tap enable/disable control.
- Add a “rewrite this draft” button that updates the composer text.
- Preserve mentions and markdown with dedicated parsing.
- Add Regency, Shakespearean, or legalistic styles.
