# ffmpeg-builds
Mirrors of FFmpeg static builds for use with LosslessCut (Windows, Linux)

For Mac see https://github.com/mifi/ffmpeg-build-script

## Make a new release

Run the [Mirror BtbN release](../../actions/workflows/mirror.yml) workflow with the FFmpeg release branch (e.g. `8.1`). It downloads the `gpl-shared` builds from [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds) for linux64, linuxarm64, win64 and winarm64, verifies their checksums and creates the release `<version>-<n>`, with the exact ffmpeg version in the release notes.

BtbN only builds the newest release branches, so check its workflow matrix first. Its `latest` builds change daily.

Then update the FFmpeg version in LosslessCut.
