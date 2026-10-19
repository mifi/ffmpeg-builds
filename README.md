# ffmpeg-builds
Mirrors of FFmpeg static builds for use with LosslessCut (Windows, Linux)

For Mac see https://github.com/mifi/ffmpeg-build-script

## Make a new release

The assets are the `gpl-shared` builds from [BtbN/FFmpeg-Builds](https://github.com/BtbN/FFmpeg-Builds) for one FFmpeg release branch, e.g. 8.1. BtbN only builds the newest release branches, so check its workflow matrix first.

```bash
v=8.1
for f in linux64-gpl-shared-$v.tar.xz win64-gpl-shared-$v.zip winarm64-gpl-shared-$v.zip; do
  curl -fLO "https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/ffmpeg-n$v-latest-$f"
done
curl -fLO https://github.com/BtbN/FFmpeg-Builds/releases/download/latest/checksums.sha256
sha256sum --ignore-missing -c checksums.sha256

# Note the exact version, for the release notes
tar -xf ffmpeg-n$v-latest-linux64-gpl-shared-$v.tar.xz && LD_LIBRARY_PATH=ffmpeg-n$v-latest-linux64-gpl-shared-$v/lib ffmpeg-n$v-latest-linux64-gpl-shared-$v/bin/ffmpeg -version | head -1

gh release create $v-1 --repo mifi/ffmpeg-builds --title $v-1 --notes "Mirror of BtbN/FFmpeg-Builds (ffmpeg <version from above>)" ffmpeg-n$v-latest-*
```

Then update the `download-ffmpeg-linux-x64` and `download-ffmpeg-win32-*` scripts in LosslessCut's `package.json` (tag, file names and extracted folder names).
