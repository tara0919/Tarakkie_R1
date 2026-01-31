# Tarakkie_R1 Build Instructions

This document explains how to build the firmware for Tarakkie_R1 using Docker.

## Prerequisites

- [Docker](https://www.docker.com/) installed and running.
- ZMK source code and config already initialized in this directory.

## Build Command (Local Docker)

Run the following command from the project root directory (Tarakkie_R1).

### For Windows (PowerShell)
```powershell
docker run --rm -v "${PWD}:/workspace" zmkfirmware/zmk-dev-arm:3.5 /bin/bash -c "export Zephyr_DIR=/workspace/zephyr/share/zephyr-package/cmake && export ZEPHYR_BASE=/workspace/zephyr && cd /workspace/zmk/app && west build -p -b seeeduino_xiao_ble -- -DSHIELD=tarakkie_R1_left -DZMK_CONFIG=/workspace/config && cp build/zephyr/zmk.uf2 /workspace/firmware/tarakkie_R1_left.uf2 && west build -p -b seeeduino_xiao_ble -- -DSHIELD=tarakkie_R1_right -DZMK_CONFIG=/workspace/config && cp build/zephyr/zmk.uf2 /workspace/firmware/tarakkie_R1_right.uf2"
```

### For Linux / macOS (bash/zsh)
```bash
docker run --rm -v "$(pwd):/workspace" zmkfirmware/zmk-dev-arm:3.5 /bin/bash -c "export Zephyr_DIR=/workspace/zephyr/share/zephyr-package/cmake && export ZEPHYR_BASE=/workspace/zephyr && cd /workspace/zmk/app && west build -p -b seeeduino_xiao_ble -- -DSHIELD=tarakkie_R1_left -DZMK_CONFIG=/workspace/config && cp build/zephyr/zmk.uf2 /workspace/firmware/tarakkie_R1_left.uf2 && west build -p -b seeeduino_xiao_ble -- -DSHIELD=tarakkie_R1_right -DZMK_CONFIG=/workspace/config && cp build/zephyr/zmk.uf2 /workspace/firmware/tarakkie_R1_right.uf2"
```

## Output Files

The built firmware files will be located in the `firmware/` directory:
- `tarakkie_R1_left.uf2`
- `tarakkie_R1_right.uf2`

## Technical Details (Environment Setup)

If you are running `west build` manually inside the container, you MUST set the following environment variables:
- `Zephyr_DIR`: `/workspace/zephyr/share/zephyr-package/cmake`
- `ZEPHYR_BASE`: `/workspace/zephyr`
- `ZMK_CONFIG`: `/workspace/config` (passed as a CMake argument `-DZMK_CONFIG=/workspace/config`)
