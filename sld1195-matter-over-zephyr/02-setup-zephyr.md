# Set Up the Zephyr Workspace

The commands in this guide use a POSIX shell and assume the West workspace is `~/workspace`.

## 1. Set Up Simplicity SDK for Zephyr

Follow the [Simplicity SDK for Zephyr Getting Started Guide](https://docs.silabs.com/zephyr/latest/zephyr-getting-started/getting-started-guide) to install the host tools, create the workspace, fetch the Silicon Labs binary blobs, and install the toolchain. For SiWx917, also flash the matching NWP firmware.

Activate the workspace's Python virtual environment before running West commands:

```sh
cd ~/workspace
source .venv/bin/activate
```

## 2. Install GN

Zephyr uses CMake, but the Matter module also uses GN to generate Ninja build files. GN must be available in your `PATH`.

Download a [prebuilt GN binary](https://chrome-infra-packages.appspot.com/p/gn/gn) for your host, or build GN from source. For example, on Linux:

```sh
git clone https://gn.googlesource.com/gn ~/gn
cd ~/gn
python3 build/gen.py
ninja -C out gn
mkdir -p ~/.local/bin
install -m 755 out/gn ~/.local/bin/gn
export PATH="$HOME/.local/bin:$PATH"
```

Verify that GN is available:

```sh
gn --version
```

## 3. Add Matter to the Workspace

The Silicon Labs setup uses `zephyr-silabs` as the manifest repository. Confirm the location:

```sh
cd ~/workspace
west config manifest.path
```

In `~/workspace/zephyr-silabs/west.yml`, add `self.import` under `manifest` to import the `submanifests` directory:

```yaml
manifest:
    self:
        import: submanifests
```

Merge this setting into the existing manifest; do not replace its projects or other settings. If your workspace uses a different manifest repository, apply this setting there instead.

Create the directory:

```sh
mkdir -p ~/workspace/zephyr-silabs/submanifests
```

Create `~/workspace/zephyr-silabs/submanifests/matter.yaml` with the following content:

```yaml
manifest:
    projects:
        - name: matter
          url: https://github.com/SiliconLabsSoftware/matter_sdk
          revision: release_2.10-1.6.1
          path: modules/lib/matter
          submodules:
              - path: third_party/editline/repo
              - path: third_party/jsoncpp/repo
              - path: third_party/nlassert/repo
              - path: third_party/nlio/repo
              - path: third_party/uriparser/repo
              - path: third_party/pigweed/repo
              - path: third_party/silabs/matter_support
```

Fetch Matter and its required submodules:

```sh
cd ~/workspace
west update
west list matter
```

Confirm that `west list matter` reports `modules/lib/matter`. If the project is not found, check the manifest import above. Matter's `zephyr/module.yml` registers it as the Zephyr module `connectedhomeip`.

## 4. Create the Pigweed Environment File

The West workflow does not run the Matter bootstrap, which normally generates `build_overrides/pigweed_environment.gni`. If the file is missing, create an empty file as a workaround:

```sh
touch ~/workspace/modules/lib/matter/build_overrides/pigweed_environment.gni
```

Continue with [All-Devices Application](03-all-devices-app.md).