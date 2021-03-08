# rules_cc_stamp

Bazel rules to aid in stamping C++ builds

## Install

```python
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "rules_cc_stamp",
    strip_prefix = "rules_cc_stamp-63d4861f4d420b574fa0f112599aae2b8aee785e",
    urls = ["https://github.com/zaucy/rules_cc_stamp/archive/63d4861f4d420b574fa0f112599aae2b8aee785e.zip"],
    sha256 = "f469a3b97eeabeb850c655f59ea17799ff40badd3a0b3e9de38534c89ad2f87d",
)
```

## Usage

### cc_stamp_header

Creates a stamped header with `constexpr` variables.

```python
load("@rules_cc_stamp//:index.bzl", "cc_stamp_header")
load("@rules_cc//cc:defs.bzl", "cc_library")

# Each stable and volatile key value pairs will be avalable as constexpr 
# variables with the same name. Configuration of the these key value pairs is
# done through the --workspace_status_command. Read more here:
# https://docs.bazel.build/versions/master/user-manual.html#flag--workspace_status_command
cc_stamp_header(
    name = "my_stamp_header",
    out = "my_stamp_header.hh",
)

cc_library(
    name = "my_library",
    srcs = ["my_library.cc", ":my_stamp_header"],
    hdrs = ["my_library.hh"],
)
```
