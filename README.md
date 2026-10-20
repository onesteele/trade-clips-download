# Trade Clips download page

The page behind https://onesteele.github.io/trade-clips-download/. It's one file, `index.html`, served by GitHub Pages from the `main` branch.

The installer isn't kept in the repository itself. The `.dmg` (136 MB) and the files that travel with it are attached to the release [v0.2.0-unsigned](https://github.com/onesteele/trade-clips-download/releases/tag/v0.2.0-unsigned). The page's Download button links straight to that file.

The app's source code stays in the private repository `RPx305/trade-clips`. This repository holds only the download page.

## Putting out a new version

1. Get the new release files from `RPx305/trade-clips`:
   ```bash
   cd ~/Documents/trade-clips-download/release-files
   gh release download <tag> -R RPx305/trade-clips --clobber
   shasum -a 256 -c SHA256SUMS.txt
   ```
2. Make the same release here with every file, because the FFmpeg source files must travel with the app (GPL):
   ```bash
   gh release create <tag> -R onesteele/trade-clips-download --title "Trade Clips <version>" --notes "..." release-files/*
   ```
3. In `index.html`, update:
   - the tag and file name in the two download links and the release-page link
   - the version and size under the button
   - the file name in step 1 of "Install it"
   - the SHA-256 line in the footer, taken from `SHA256SUMS.txt`

   Then commit and push. Pages updates within a minute or two.

Once Reece's builds are notarised by Apple, the "first time only" and "Still won't open?" sections can come out.
