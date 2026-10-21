# Trade Clips download page

The page behind https://onesteele.github.io/trade-clips-download/. It's one file, `index.html`, served by GitHub Pages from the `main` branch.

The installer isn't kept in the repository itself. The `.dmg` (322 MB) and the files that travel with it are attached to the release [v0.5.0-unsigned](https://github.com/onesteele/trade-clips-download/releases/tag/v0.5.0-unsigned). The page's Download button links straight to that file. Older releases stay on the [releases page](https://github.com/onesteele/trade-clips-download/releases).

The app's source code stays private: Reece's repository `RPx305/trade-clips` and the fork `onesteele/trade-clips`. This repository holds only the download page.

## Putting out a new version

Each release's files go in their own folder, `release-files/<tag>/`. That folder is ignored by git.

1. Get the release files, either way:
   - **Reece's release:**
     ```bash
     mkdir -p ~/Documents/trade-clips-download/release-files/<tag> && cd "$_"
     gh release download <tag> -R RPx305/trade-clips --clobber
     shasum -a 256 -c SHA256SUMS.txt
     ```
   - **A version built on this Mac** (0.3.0, 0.4.1 and 0.5.0 were built from `~/Documents/trade-clips`): bump `version` in its `package.json`, then run `npm run package` and `npm run handoff`. Copy the files out of `release/handoff/Trade Clips <version>/` with hyphens instead of spaces, because GitHub renames spaces:
     - `Trade-Clips-<version>-arm64.dmg`
     - `How-to-install-Trade-Clips.pdf`
     - from `FFmpeg source code/`: the four tarballs, `ffmpeg-build.txt` and `COPYING.GPLv2`, plus `README.txt` renamed to `FFmpeg-source-README.txt`

     Then write `SHA256SUMS.txt` with `shasum -a 256` over the `.dmg`, the tarballs, `ffmpeg-build.txt` and `COPYING.GPLv2`.
2. Make the same release here with every file, because the FFmpeg source files must travel with the app (GPL):
   ```bash
   gh release create <tag> -R onesteele/trade-clips-download --title "Trade Clips <version> (not yet notarised)" --notes "..." release-files/<tag>/*
   ```
3. In `index.html`, update:
   - the tag and file name in the two download links and the release-page link
   - the version and size under the button
   - the file name in step 1 of "Install it"
   - the SHA-256 line in the footer, taken from `SHA256SUMS.txt`

   Then commit and push. Pages updates within a minute or two.

Once Reece's builds are notarised by Apple, the "first time only" and "Still won't open?" sections can come out.
