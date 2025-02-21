load("//tensorflow/tsl/platform/default:distribute.bzl", "distribute_py_test")

package(
    default_visibility = ["//tensorflow:internal"],
    licenses = ["notice"],
)

# Pybind rules must live in tensorflow/python due to header rule visibility.
exports_files(
    ["pywrap_parallel_device.cc"],
    visibility = ["//tensorflow/python:__pkg__"],
)

py_library(
    name = "parallel_device",
    srcs = ["parallel_device.py"],
    srcs_version = "PY3",
    visibility = [
        "//tensorflow:internal",
        "//third_party/py/tensorflow_numerics/extensions:__pkg__",
    ],
    deps = [
        "//tensorflow/python:_pywrap_parallel_device",
        "//tensorflow/python/distribute:device_util",
        "//tensorflow/python/tpu/ops",
    ],
)

distribute_py_test(
    name = "parallel_device_test",
    srcs = ["parallel_device_test.py"],
    # We don't only use TPU Runtime on parallel device, we use c_api_tfrt instead.
    disable_tpu_use_tfrt = True,
    python_version = "PY3",
    tags = [
        # Dependencies aren't otherwise included in the pip package yet.
        "no_pip",
        "notpu",  # TODO(b/210159281)
    ],
    deps = [
        ":parallel_device",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:collective_ops",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python/module",
        "//tensorflow/python/tpu",
    ],
)
