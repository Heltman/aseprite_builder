# What is it
Automated workflow for GitHub Actions which builds Aseprite for macOS and Windows.</br>
By using GitHub actions there is no need for manual compilation and it does not contain malware.</br>
To adhere to the EULA of Aseprite, this workflow does not upload the binary in a public accessible space like artifacts.</br>
The release can be found within the releases as a draft (only visible for repo owner).

# How to use
1. Clone or fork this repo
2. Edit /.github/workflows/aseprite_build_deploy.yml
3. Find and edit the **os** line and remove the os you don't need.

        strategy:
            matrix:
                os: [macos-latest, windows-latest]
4. Save and commit.
5. Run the workflow manually (Actions → Build and deploy Aseprite → Run workflow).
   Uncomment the `schedule`/`push` triggers if you want it to check for new Aseprite releases on its own.

# Technical details
This workflow follows the instructions as described at [Aseprite repo](https://github.com/aseprite/aseprite/blob/master/INSTALL.md)

1. Ask GitHub for the latest Aseprite release and download its source archive.
2. Create a draft Release for that version (skipped if it already exists).
3. Skip the build when every platform asset is already attached (pass `force` to rebuild anyway).
4. Download the Skia build that the source itself asks for (`laf/misc/skia-tag.txt`).
5. Use CMake and Ninja to compile, then package `Aseprite.app` (macOS) or a portable folder (Windows).
6. Upload the zip to the draft Release, replacing an older asset of the same name.

# Build times
Every month you have 2000 free minutes from GitHub.</br>
Different Operating Systems costs different amounts of minutes, see [billing for GitHub Actions](https://help.github.com/en/github/setting-up-and-managing-billing-and-payments-on-github/about-billing-for-github-actions#about-billing-for-github-actions)</br>
So building for all three Operating Systems will cost 130 minutes (20 * 2+10 * 1+8 * 10)</br>
That is why we recommend you to modify the **os** line to only build for the OS that you need.
|Operating System|Minutes|Minute multiplier
|---|---|---|
|Windows|20|2|
|Ubuntu|10|1|
|macOS|8|10|

# References to other Aseprite builders
- https://github.com/haxpor/aseprite-macos-buildsh => Script which lets you build automatically on macOS
- https://github.com/Insouciant21/action_aseprite => Uses GitHub Actions, but currently has unoptimized binaries and these are publicly available which goes against Aseprite EULA

# Support Aseprite
Keep supporting Aseprite at https://aseprite.org/#buy
