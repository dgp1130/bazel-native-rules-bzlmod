# Bazel `--incompatible_disable_native_repo_rules` + `--noenable_bzlmod`

This is an empty workspace with a [`.bazelrc`](/.bazelrc) file which sets both:
1.  `--incompatible_disable_native_repo_rules`
2.  `--noenable_bzlmod`

It has an empty [`foo.txt`](/foo.txt) file to create a target to build. When
building this file, Bazel emits:

> ERROR: /DEFAULT.WORKSPACE:1:17: fetching local_repository rule //external:bazel_tools: Native repo rule local_repository is disabled since the flag --incompatible_disable_native_repo_rules is set. Native repo rules are deprecated; please migrate to their Starlark counterparts. For local_repository, please use load("@bazel_tools//tools/build_defs/repo:local.bzl", "local_repository").
> ERROR: Error computing the main repository mapping: no such package '@@bazel_tools//tools/build_defs/repo': Native repo rule local_repository is disabled since the flag --incompatible_disable_native_repo_rules is set. Native repo rules are deprecated; please migrate to their Starlark counterparts. For local_repository, please use load("@bazel_tools//tools/build_defs/repo:local.bzl", "local_repository").

Disabling either flag fixes the error. Note that the
[`WORKSPACE.bazel`](/WORKSPACE.bazel) file is completely empty, so this cannot
be referring to any error inside this project.
