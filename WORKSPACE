workspace(name = "test")
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive", "http_jar", "http_file")


skylib_version = "1.0.3"
http_archive(
    name = "bazel_skylib",
    urls = [
    "https://repository.rubrik.com/artifactory/github/bazelbuild/bazel-skylib/releases/download/%s/bazel-skylib-%s.tar.gz" % (skylib_version, skylib_version),
    ],
    sha256 = "1c531376ac7e5a180e0237938a2536de0c54d93f5c278634818e0efc952dd56c",
)
load("@bazel_skylib//:workspace.bzl", "bazel_skylib_workspace")
bazel_skylib_workspace()

rules_scala_version = "376765b8cb2b82d201b05f359d3b4faa6229eefa"
http_archive(
    name = "io_bazel_rules_scala",
    url = "https://repository.rubrik.com/artifactory/github/bazelbuild/rules_scala/archive/%s.zip" % rules_scala_version,
    strip_prefix= "rules_scala-%s" % rules_scala_version,
    sha256 = "5d3cbe75503af9a4c9ac2905c46326ce7364fe2124f0441265fcbdf12003c0d0",
)

scala_version = "2.12.11"

load("@io_bazel_rules_scala//:scala_config.bzl", "scala_config")
scala_config(scala_version=scala_version)

register_toolchains("//build_rules:scala_toolchain")

load("@io_bazel_rules_scala//testing:scalatest.bzl", "scalatest_toolchain")
scalatest_toolchain()

load("@io_bazel_rules_scala//scala:scala.bzl", "scala_repositories")
scala_repositories()

load("@io_bazel_rules_scala//scala_proto:scala_proto.bzl", "scala_proto_repositories")
scala_proto_repositories()

register_toolchains("//build_rules:scalapb_toolchain")

load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")

# Declares @com_google_protobuf//:protoc pointing to released binary
# This should stop building protoc during bazel build
# See https://github.com/bazelbuild/rules_proto/pull/36
rules_proto_dependencies()
rules_proto_toolchains()
