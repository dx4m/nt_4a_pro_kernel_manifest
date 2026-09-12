# Nothing Phone (4a) Pro Kernel Build Manifest

It gets the complete buildchain from different sources.

## How to setup

Open a new shell:

```sh
mkdir nt_kernel_build && cd nt_kernel_build
repo init --depth=1 -u https://github.com/dx4m/nt_4a_pro_kernel_manifest.git
repo sync
```

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

## Bazel Wrapper?

So basically the bazel wrapper runs, gets all dependencies like KSU and patches stamp and gki_defconfig on the fly, then runs the real bazel, and after that, it returns to the wrapper, resignes the boot.img, and cleans up what it patched.
