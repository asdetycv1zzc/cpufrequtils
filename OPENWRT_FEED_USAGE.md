# cpufrequtils OpenWrt feed packaging

This repository now includes an OpenWrt package definition at:

- `package/utils/cpufrequtils/Makefile`

## How to use as a local src-link feed

In your OpenWrt source tree:

```sh
echo "src-link cpufrequtils /absolute/path/to/cpufrequtils" >> feeds.conf.default
./scripts/feeds update cpufrequtils
./scripts/feeds install -p cpufrequtils cpufrequtils libcpufreq
make menuconfig
```

Then enable:

- `Utilities -> cpufrequtils`
- `Libraries -> libcpufreq`

and build.

## Notes

- The package now builds from local feed source files and does not fetch source from GitHub during package build.
- `src-link` path must be an absolute path.
