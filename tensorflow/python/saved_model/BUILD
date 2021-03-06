# Description:
# TensorFlow SavedModel.

package(
    # TODO(drpng): change that to //third_party/tensorflow:internal
    # when we have migrated all users.
    default_visibility = ["//visibility:public"],
)

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

load("//tensorflow:tensorflow.bzl", "tf_py_test")
load("//tensorflow/core:platform/default/build_config.bzl", "tf_proto_library")
load("//tensorflow/core:platform/default/build_config.bzl", "tf_additional_all_protos")

py_library(
    name = "saved_model",
    srcs = ["saved_model.py"],
    srcs_version = "PY2AND3",
    visibility = ["//tensorflow:internal"],
    deps = [
        ":builder",
        ":constants",
        ":load",
        ":loader",
        ":main_op",
        ":save",
        ":signature_constants",
        ":signature_def_utils",
        ":simple_save",
        ":tag_constants",
        ":utils",
        "//tensorflow/python:util",
    ],
)

py_library(
    name = "constants",
    srcs = ["constants.py"],
    srcs_version = "PY2AND3",
    deps = ["//tensorflow/python:util"],
)

py_library(
    name = "signature_constants",
    srcs = ["signature_constants.py"],
    srcs_version = "PY2AND3",
    deps = ["//tensorflow/python:util"],
)

py_library(
    name = "tag_constants",
    srcs = ["tag_constants.py"],
    srcs_version = "PY2AND3",
    deps = ["//tensorflow/python:util"],
)

py_library(
    name = "builder",
    srcs = [
        "builder.py",
        "builder_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lib",
        "//tensorflow/python:platform",
        "//tensorflow/python:training",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
    ],
)

py_library(
    name = "loader",
    srcs = [
        "loader.py",
        "loader_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        ":signature_def_utils",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lib",
        "//tensorflow/python:platform",
        "//tensorflow/python:saver",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
    ],
)

tf_py_test(
    name = "loader_test",
    size = "small",
    srcs = ["loader_test.py"],
    additional_deps = [
        ":builder",
        ":loader",
        ":signature_def_utils",
        ":utils",
        "@absl_py//absl/testing:parameterized",
        "//tensorflow/python:client",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:errors",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:lib",
        "//tensorflow/python:state_ops",
        "//tensorflow/python:training",
        "//tensorflow/python:variables",
    ],
)

py_library(
    name = "simple_save",
    srcs = [
        "simple_save.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":builder",
        ":signature_constants",
        ":signature_def_utils",
        ":tag_constants",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:lib",
        "//tensorflow/python:util",
    ],
)

py_library(
    name = "main_op",
    srcs = [
        "main_op.py",
        "main_op_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lookup_ops",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
    ],
)

tf_py_test(
    name = "saved_model_test",
    size = "small",
    srcs = ["saved_model_test.py"],
    additional_deps = [
        ":builder",
        ":constants",
        ":loader",
        ":main_op",
        ":signature_def_utils",
        ":tag_constants",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:errors",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:framework_test_lib",
        "//tensorflow/python:lib",
        "//tensorflow/python:math_ops",
        "//tensorflow/python:saver_test_utils",
        "//tensorflow/python:session",
        "//tensorflow/python:state_ops",
        "//tensorflow/python:test_ops",
        "//tensorflow/python:training",
        "//tensorflow/python:util",
        "//tensorflow/python:variables",
    ],
    data = ["//tensorflow/cc/saved_model:saved_model_half_plus_two"],
    tags = ["no_windows"],
)

py_library(
    name = "utils",
    srcs = [
        "utils.py",
        "utils_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:lib",
        "//tensorflow/python:sparse_tensor",
        "//tensorflow/python:util",
    ],
)

tf_py_test(
    name = "utils_test",
    size = "small",
    srcs = ["utils_test.py"],
    additional_deps = [
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_for_generated_wrappers",
        "//tensorflow/python:sparse_tensor",
    ],
)

py_library(
    name = "signature_def_utils",
    srcs = [
        "signature_def_utils.py",
        "signature_def_utils_impl.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":signature_constants",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:util",
    ],
)

tf_py_test(
    name = "signature_def_utils_test",
    size = "small",
    srcs = ["signature_def_utils_test.py"],
    additional_deps = [
        ":signature_constants",
        ":signature_def_utils",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_for_generated_wrappers",
    ],
)

tf_py_test(
    name = "simple_save_test",
    size = "small",
    srcs = ["simple_save_test.py"],
    additional_deps = [
        ":loader",
        ":signature_constants",
        ":simple_save",
        ":tag_constants",
        "//tensorflow/python:client_testlib",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:variables",
    ],
)

py_library(
    name = "save",
    srcs = [
        "save.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":builder",
        ":constants",
        ":function_serialization",
        ":saved_object_graph_py",
        ":signature_constants",
        ":signature_def_utils",
        ":tag_constants",
        ":utils",
        "//tensorflow/core:protos_all_py",
        "//tensorflow/python:array_ops",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:control_flow_ops",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:framework",
        "//tensorflow/python:framework_ops",
        "//tensorflow/python:lib",
        "//tensorflow/python:resource_variable_ops",
        "//tensorflow/python:tensor_spec",
        "//tensorflow/python:util",
        "//tensorflow/python/eager:context",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:function",
        "//tensorflow/python/training/checkpointable:base",
        "//tensorflow/python/training/checkpointable:tracking",
        "//tensorflow/python/training/checkpointable:util",
    ],
)

tf_py_test(
    name = "save_test",
    srcs = ["save_test.py"],
    additional_deps = [
        ":loader",
        ":save",
        ":signature_constants",
        ":tag_constants",
        "@absl_py//absl/testing:parameterized",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:test",
    ],
)

py_library(
    name = "load",
    srcs = [
        "load.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":constants",
        ":function_deserialization",
        ":loader",
        ":saved_object_graph_py",
        ":utils",
        "//tensorflow/python:function",
        "//tensorflow/python:lib",
        "//tensorflow/python:util",
        "//tensorflow/python/training/checkpointable:tracking",
    ],
)

tf_py_test(
    name = "load_test",
    srcs = ["load_test.py"],
    additional_deps = [
        ":load",
        ":save",
        "//tensorflow/python:constant_op",
        "//tensorflow/python:dtypes",
        "//tensorflow/python:lib",
        "//tensorflow/python:tensor_spec",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:test",
        "//tensorflow/python/training/checkpointable:tracking",
    ],
)

py_library(
    name = "function_serialization",
    srcs = [
        "function_serialization.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":nested_structure_coder",
        ":saved_object_graph_py",
        "//tensorflow/python/eager:def_function",
        "//tensorflow/python/eager:function",
    ],
)

py_library(
    name = "function_deserialization",
    srcs = [
        "function_deserialization.py",
    ],
    srcs_version = "PY2AND3",
    deps = [
        ":nested_structure_coder",
        "//tensorflow/python/eager:def_function",
    ],
)

tf_proto_library(
    name = "struct",
    srcs = ["struct.proto"],
    cc_api_version = 2,
    protodeps = tf_additional_all_protos(),
    visibility = ["//tensorflow:internal"],
)

tf_proto_library(
    name = "saved_object_graph",
    srcs = ["saved_object_graph.proto"],
    cc_api_version = 2,
    protodeps = tf_additional_all_protos() + [":struct"],
    visibility = ["//tensorflow:internal"],
)

py_library(
    name = "nested_structure_coder",
    srcs = ["nested_structure_coder.py"],
    deps = [
        ":struct_py",
        "//tensorflow/python:framework",
        "@six_archive//:six",
    ],
)

tf_py_test(
    name = "nested_structure_coder_test",
    srcs = ["nested_structure_coder_test.py"],
    additional_deps = [
        ":nested_structure_coder",
        ":struct_py",
        "//tensorflow/python:framework",
        "//tensorflow/python/eager:test",
    ],
)
