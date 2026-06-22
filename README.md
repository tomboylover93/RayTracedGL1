# RTGL1

This README has instructions for building the RayTracedGL1 library on Linux (doom branch for prboom-plus-rt). For the original README see README_ORIG.md.

## Dependencies

**Debian/Ubuntu**
```bash
sudo apt install build-essential cmake libvulkan-dev python3 glslang-tools
```

**Fedora**
```bash
sudo dnf install cmake gcc-c++ vulkan-devel python3 glslang
```

**Arch Linux**
```bash
sudo pacman -S --needed base-devel cmake vulkan-devel python glslang
```

## Build

Clone the repository and run cmake:

```bash
git clone https://github.com/tomboylover93/RayTracedGL1 -b doom
cd RayTracedGL1
cmake -S . -B build \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DRG_WITH_SURFACE_XLIB=ON \
  -DRG_WITH_SURFACE_WAYLAND=ON
cmake --build build -j$(nproc)
```

The `-DRG_WITH_SURFACE_*` flags enable Vulkan surface support for the corresponding display servers. At minimum you'll need `XLIB` for X11 or `WAYLAND` for Wayland. You can enable both.

### NVIDIA DLSS (optional)

Add `-DRG_WITH_NVIDIA_DLSS=ON` to the cmake command. You also need the [NVIDIA DLSS SDK](https://github.com/NVIDIA/DLSS) (DLSS 2.x) with pre-built .so files downloaded and the `DLSS_SDK_PATH` environment variable set.

### Shaders

Run `GenerateShaders.py` to compile the shaders:

```bash
python3 GenerateShaders.py
```

They will be available in the `Build` (case-sensitive) directory.

## Output

The build produces `build/libRayTracedGL1.so`. Set `RTGL1_SDK_PATH` to the repository root when building prboom-plus-rt:

```bash
export RTGL1_SDK_PATH=/path/to/RayTracedGL1
```

# License

The code in this repository is licensed under the MIT License. See the LICENSE file for details.
