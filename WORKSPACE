load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

# rules for NodeJS
git_repository(
    name = "build_bazel_rules_nodejs",
    remote = "https://github.com/bazelbuild/rules_nodejs.git",
    tag = "0.16.2",
)

load("@build_bazel_rules_nodejs//:package.bzl", "rules_nodejs_dependencies")
rules_nodejs_dependencies()

load("@build_bazel_rules_nodejs//:defs.bzl", "node_repositories", "yarn_install")

node_repositories()

yarn_install(
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)
