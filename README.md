# TerminalCraft GitHub Offline Builder

This is for Macs where Minecraft/Mojang downloads work in the browser but are
blocked from Terminal/Python.

GitHub Actions downloads the files on GitHub's servers and packages a complete
vanilla Minecraft installation for macOS ARM64.

## What it downloads

- The official Minecraft version JSON
- The official client JAR
- Java libraries
- macOS ARM64 native libraries
- Extracted macOS ARM64 natives
- Logging configuration
- Asset index
- Minecraft asset objects

It does NOT include Microsoft account credentials.

## Set it up using only the GitHub website

1. Create a new GitHub repository. A private repository is fine if your account
   has Actions minutes available.

2. Choose **Add file -> Create new file**.

3. For the filename, enter exactly:

   `.github/workflows/build.yml`

4. Copy the contents of `build.yml` from this package into the editor.

5. Commit the file.

6. Open the repository's **Actions** tab.

7. Open **Build TerminalCraft Minecraft Files**.

8. Click **Run workflow**.

9. Leave the version as `1.21.11` (or enter another version) and run it.

10. Wait for the workflow to finish.

11. At the bottom of the finished workflow page, download the artifact named:

    `TerminalCraft-1.21.11-macOS-ARM64`

GitHub downloads an outer artifact ZIP. Extract it. Inside is another file:

`TerminalCraft-1.21.11-macOS-ARM64.zip`

Extract that too.

You will then have a folder named:

`minecraft`

## Merge it into TerminalCraft

Suppose the extracted `minecraft` folder is in Downloads.

Run:

```bash
SRC="$HOME/Downloads/minecraft"
DST="$HOME/Library/Application Support/TerminalCraft/minecraft"

mkdir -p "$DST"
ditto "$SRC" "$DST"
```

If your extracted folder has a different location, adjust `SRC`.

Then launch TerminalCraft again.

## Verify the library that caused the first crash

```bash
ls "$HOME/Library/Application Support/TerminalCraft/minecraft/libraries/net/sf/jopt-simple/jopt-simple/5.0.4/"
```

You should see:

`jopt-simple-5.0.4.jar`

The builder also creates:

`versions/1.21.11/natives/`

so TerminalCraft has the native macOS ARM64 files needed by LWJGL.
