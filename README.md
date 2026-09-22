# Nothing Phone (4a) Pro Kernel Build Manifest

It gets the complete buildchain from different sources to compile a custom Kernel.

## How to setup

Open a new shell:

```sh
mkdir nt_kernel_build && cd nt_kernel_build
repo init --depth=1 -u https://github.com/dx4m/nt_4a_pro_kernel_manifest.git
repo sync
```

## How to build

When finished you can pick one of the following commands to build the kernel:

```sh
tools/bazel run --config=stamp //froggerpro:kernel
tools/bazel run --config=stamp //froggerpro:kernel_ksu
tools/bazel run --config=stamp //froggerpro:kernel_ksun
tools/bazel run --config=stamp //froggerpro:kernel_sukisu
tools/bazel run --config=stamp //froggerpro:kernel_resukisu
```

and with susfs

```sh
tools/bazel run --config=stamp //froggerpro:kernel_ksu_susfs
tools/bazel run --config=stamp //froggerpro:kernel_ksun_susfs
tools/bazel run --config=stamp //froggerpro:kernel_sukisu_susfs
tools/bazel run --config=stamp //froggerpro:kernel_resukisu_susfs
```

or use

```sh
tools/bazel run --config=stamp //msm-kernel:sun_perf_dist
```

without any patches from the bazel wrapper.

## Build with Github Actions

You can build it through actions. Just fork it, setup write permission, go to Actions, click on "Manual Kernel Build" and click on "Run workflow".
Then select your settings and hit the green "Run workflow". Keep in mind, Github Runners take up to an hour to finish.
Self-Hosted runners are quicker, but need more setup and your own hardware. For more information read the docs ***[here](https://docs.github.com/en/actions/concepts/runners/self-hosted-runners)***

## Bazel Wrapper?

So basically the bazel wrapper runs, gets all dependencies like KSU and patches stamp and gki_defconfig on the fly, then runs the real bazel, and after that, it returns to the wrapper, resignes the boot.img, and cleans up what it patched.
