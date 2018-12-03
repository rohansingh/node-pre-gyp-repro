node-pre-gyp-repro
===

Repros the issue described in https://github.com/mapbox/node-pre-gyp/issues/433.

Usage
---
This will trigger the issue:
```
bazel build //:rebuild
```

Notes
---
The issue seems to hinge around having this line in the build script:
```
export npm_config_target_libc=glibc
```

After removing that from the `genrule` in `BUILD`, everything works perfectly.
