# bazel-cant-find-python

This repository minimally demonstrates an unexpected behavior when using the
`bazel` build system with [asdf-vm](https://asdf-vm.com/#/).

It appears that the `rules_docker` rules rely on `python` to build docker
images.

If you use `asdf-vm` for installing and managing your version of `python`, it
doesn't appear that `rules_docker` respects the shimming that `asdf-vm` does in
order to let you define different installations of `python`.

## Build Output

```
⇒  bazel build //cmd:image
INFO: Analyzed target //cmd:image (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
ERROR: /home/aaron/.cache/bazel/_bazel_aaron/0af56278f10e6cbad2a360a8f1460ff0/external/distroless_base/image/BUILD:4:17: SHA256 external/distroless_base/image/001.tar.gz.nogz.sha256 failed (Exit 1) sha256 failed: error executing command bazel-out/host/bin/external/bazel_tools/tools/build_defs/hash/sha256 bazel-out/k8-fastbuild/bin/external/distroless_base/image/001.tar.gz.nogz ... (remaining 1 argument(s) skipped)

Use --sandbox_debug to see verbose messages from the sandbox
unknown command: python. Perhaps you have to reshim?
Target //cmd:image failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 0.226s, Critical Path: 0.09s
INFO: 0 processes.
FAILED: Build did NOT complete successfully
```

## Versions

Both `python` and `bazel` themselves are installed with `asdf-vm`.

```
⇒  cat .tool-versions
python 3.8.5 2.7.16
bazel 3.5.0
```
