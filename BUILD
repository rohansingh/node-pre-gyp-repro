load("@bazel_tools//tools/build_defs/pkg:pkg.bzl", "pkg_tar")

pkg_tar(
    name = "node_modules",
    strip_prefix = ".",
    package_dir = "/discarded",

    srcs = ["@npm//:node_modules"],
)

genrule(
    name = "rebuild",
    message = "Rebuilding node_modules for target platform",
    srcs = [":node_modules.tar"],
    tools = [
        "package.json",
        "yarn.lock",
        "@nodejs//:bin/npm",
    ],
    outs = ["rebuild.tar"],

    tags = ["local"], # run without sandboxing

    cmd = """
    NPM="$$(pwd)/$(location @nodejs//:bin/npm)"

    # extract node_mdules.tar and package.json
    tar xf $< -C $(@D)
    cp $(location //:package.json) $(@D)
    cp $(location //:yarn.lock) $(@D)

    (
        cd $(@D)/npm/

        # test connectivity
        curl google.com

        # removing this export fixes the problem
        export npm_config_target_libc=glibc

        # rebuild
        $$NPM rebuild --update-binary \
            --target_arch=x64 --target_platform=linux
    )

    tar cf $@ $(@D)/npm/node_modules
    """,
)
