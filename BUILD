# This depends on bar, but doesn't actually use it.
# This is a bit of a contrived example, but this can
# happen legitimately if its far down the dependency tree.
cc_library(
    name = "foo",
    srcs = ["foo.cpp"],
    hdrs = ["foo.hpp"],
    deps = [":bar"],
)

cc_library(
    name = "bar",
    srcs = ["bar.cpp"],
    hdrs = ["bar.hpp"],
)

cc_shared_library(
    name = "foo_shared",
    deps = [":foo"],
    exports_filter = ["//:__pkg__"],
)

# This uses both foo and bar. Since bar is in the exports_filter of foo, this
# is only linked into foo_shared and not into bin. However, the linker drops
# bar since it isn't used.
cc_binary(
    name = "bin",
    srcs = ["bin.cpp"],
    deps = [":foo", ":bar"],
    dynamic_deps = [":foo_shared"],
)