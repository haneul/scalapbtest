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

rules_scala_version = "c96948c77825e3d5ce00b9711bff6c349477e37f"
http_archive(
    name = "io_bazel_rules_scala",
    url = "https://repository.rubrik.com/artifactory/github/bazelbuild/rules_scala/archive/%s.zip" % rules_scala_version,
    strip_prefix= "rules_scala-%s" % rules_scala_version,
    sha256 = "bd74d16491c79e9da1cbb2b07a35a0782dd7dfbe5acd8c749225db4e6a665944",
)

scala_version = "2.12.14"

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
