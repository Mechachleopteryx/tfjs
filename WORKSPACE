load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "fcc6dccb39ca88d481224536eb8f9fa754619676c6163f87aa6af94059b02b12",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/3.2.0/rules_nodejs-3.2.0.tar.gz"],
)

load("@build_bazel_rules_nodejs//:index.bzl", "yarn_install")
yarn_install(
    name = "npm",
    package_json = "//:package.json",
    yarn_lock = "//:yarn.lock",
)

# Make all files under $HOME/emsdk/* visible to the toolchain. The files are
# available as external/emsdk/emsdk/*
load("//toolchain:cc_toolchain_config.bzl", "emsdk_configure")
emsdk_configure(name = "emsdk")

load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")
# xnnpack used for fast vectorized wasm operations
git_repository(
    name = "xnnpack",
    commit = "8772714a417ed71ff87ccf5014f6bee9d911db21",
    remote = "https://github.com/google/XNNPACK.git",
    shallow_since = "1593037483 -0700",
)

# The libraries below are transitive dependencies of XNNPACK that we need to
# explicitly enumerate here. See https://docs.bazel.build/versions/master/external.html#transitive-dependencies

# FP16 library, used for half-precision conversions
http_archive(
    name = "FP16",
    build_file = "@xnnpack//third_party:FP16.BUILD",
    sha256 = "0d56bb92f649ec294dbccb13e04865e3c82933b6f6735d1d7145de45da700156",
    strip_prefix = "FP16-3c54eacb74f6f5e39077300c5564156c424d77ba",
    urls = [
        "https://github.com/Maratyszcza/FP16/archive/3c54eacb74f6f5e39077300c5564156c424d77ba.zip",
    ],
)

# FXdiv library, used for repeated integer division by the same factor
http_archive(
    name = "FXdiv",
    sha256 = "ab7dfb08829bee33dca38405d647868fb214ac685e379ec7ef2bebcd234cd44d",
    strip_prefix = "FXdiv-b408327ac2a15ec3e43352421954f5b1967701d1",
    urls = [
        "https://github.com/Maratyszcza/FXdiv/archive/b408327ac2a15ec3e43352421954f5b1967701d1.zip",
    ],
)

# pthreadpool library, used for parallelization
http_archive(
    name = "pthreadpool",
    sha256 = "03312bd7d8d9e379d685258963ee8820767158b5946cdd00336ff17dae851001",
    strip_prefix = "pthreadpool-029c88620802e1361ccf41d1970bd5b07fd6b7bb",
    urls = [
        "https://github.com/Maratyszcza/pthreadpool/archive/029c88620802e1361ccf41d1970bd5b07fd6b7bb.zip",
    ],
)

# clog library, used for logging
http_archive(
    name = "clog",
    build_file = "@xnnpack//third_party:clog.BUILD",
    sha256 = "3f2dc1970f397a0e59db72f9fca6ff144b216895c1d606f6c94a507c1e53a025",
    strip_prefix = "cpuinfo-d5e37adf1406cf899d7d9ec1d317c47506ccb970",
    urls = [
        "https://github.com/pytorch/cpuinfo/archive/d5e37adf1406cf899d7d9ec1d317c47506ccb970.tar.gz",
    ],
)

# cpuinfo library, used for detecting processor characteristics
http_archive(
    name = "cpuinfo",
    build_file = "@xnnpack//third_party:cpuinfo.BUILD",
    patches = ["@xnnpack//third_party:cpuinfo.patch"],
    sha256 = "b1f2ee97e46d8917a66bcb47452fc510d511829556c93b83e06841b9b35261a5",
    strip_prefix = "cpuinfo-6cecd15784fcb6c5c0aa7311c6248879ce2cb8b2",
    urls = [
        "https://github.com/pytorch/cpuinfo/archive/6cecd15784fcb6c5c0aa7311c6248879ce2cb8b2.zip",
    ],
)

# psimd library, used for fallback 128-bit SIMD micro-kernels
http_archive(
    name = "psimd",
    build_file = "@xnnpack//third_party:psimd.BUILD",
    sha256 = "dc615342bcbe51ca885323e51b68b90ed9bb9fa7df0f4419dbfa0297d5e837b7",
    strip_prefix = "psimd-072586a71b55b7f8c584153d223e95687148a900",
    urls = [
        "https://github.com/Maratyszcza/psimd/archive/072586a71b55b7f8c584153d223e95687148a900.zip",
    ],
)

git_repository(
    name = "com_google_googletest",
    commit = "cd17fa2abda2a2e4111cdabd62a87aea16835014",
    remote = "https://github.com/google/googletest.git",
)

http_archive(
    name = "rules_cc",
    sha256 = "90d5a66950b492cbf86201cdc49c4b59796a85a4eb9fd63c07afe5f7132ea623",
    strip_prefix = "rules_cc-8346df34b6593b051403b8e429db15c7f4ead937",
    urls = [
        "https://github.com/bazelbuild/rules_cc/archive/8346df34b6593b051403b8e429db15c7f4ead937.zip",
    ],
)
