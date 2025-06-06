load("@io_bazel_stardoc//stardoc:stardoc.bzl", "stardoc")

# Copyright 2018 The Bazel Authors. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
load("//src/main/starlark/release:packager.bzl", "release_archive")

release_archive(
    name = "pkg",
    srcs = glob(
        ["*.bzl"],
        exclude = [
            "repositories.doc.bzl",
        ],
    ),
    src_map = {
        "BUILD.release.bazel": "BUILD.bazel",
    },
    deps = [
        "//kotlin/compiler:pkg",
        "//kotlin/internal:pkg",
        "//kotlin/settings:pkg",
    ],
)

[
    stardoc(
        name = doc,
        out = "%s.md" % doc,
        input = "%s.bzl" % doc,
        deps = [
            "//kotlin/internal",
        ],
    )
    for doc in [
        "jvm",
        "lint",
        "core",
        "repositories.doc",
    ]
]

genrule(
    name = "stardoc",
    srcs = [doc for doc in [
        "jvm",
        "lint",
        "core",
        "repositories.doc",
    ]],
    outs = ["kotlin.md"],
    cmd = """
    for md in $(SRCS); do
      cat "$$md" >> $@
    done
    """,
    executable = True,
    visibility = [
        "//visibility:public",
    ],
)
