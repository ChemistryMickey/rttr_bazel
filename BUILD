package(default_visibility = ["//visibility:public"])

# --------------------------------------------------------------------
# Header files
# --------------------------------------------------------------------
filegroup(
    name = "headers",
    srcs = glob([
            "src/rttr/**/*",
    ],
        exclude = [
            # Exclude C++ sources
            "*.cpp",
        ],
    ),
)

# --------------------------------------------------------------------
# All RTTR .cpp sources
# --------------------------------------------------------------------
rttr_srcs = glob(["src/rttr/**/*.cpp"])

# --------------------------------------------------------------------
# Common compile flags
# --------------------------------------------------------------------
rttr_copts = [
    # "-DRTTR_DISABLE_WARNINGS",
    "-DRTTR_DLL",           # needed for shared lib
    "-DRTTR_COMPILER_GCC",
    "-fPIC",
    "-O3",
    "-w", # Suppress all warnings
]

# --------------------------------------------------------------------
# Static library (librttr_core.a)
# --------------------------------------------------------------------
cc_library(
    name = "rttr_core_static",
    srcs = rttr_srcs,
    hdrs = [":headers"],
    copts = rttr_copts,
    linkstatic = True,
    strip_include_prefix = "src",
    include_prefix = "",
)

# --------------------------------------------------------------------
# Shared library (librttr_core.so)
# --------------------------------------------------------------------
cc_library(
    name = "rttr_core_shared",
    srcs = rttr_srcs,
    hdrs = [":headers"],
    copts = rttr_copts + ["-fvisibility=hidden"],
    linkstatic = False,
    strip_include_prefix = "src",
    include_prefix = "",
    linkopts = [
        "-Wl,--no-undefined",
    ],
    alwayslink = True,
)

# --------------------------------------------------------------------
# Alias: choose static by default, like CMake "rttr::rttr_core"
# --------------------------------------------------------------------
alias(
    name = "rttr_core",
    actual = ":rttr_core_static",
)
