load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
http_archive(
    name = "io_tweag_rules_nixpkgs",
    strip_prefix = "rules_nixpkgs-acb9e36f403ec6f38bac81290781cb896f22a85e",
    urls = ["https://github.com/tweag/rules_nixpkgs/archive/acb9e36f403ec6f38bac81290781cb896f22a85e.tar.gz"],
    sha256 = "52c5ab0b68841b96463e1bd44760ef2bbbffa0804873496b6e0f982f5b3176f6",
)

load("@io_tweag_rules_nixpkgs//nixpkgs:repositories.bzl", "rules_nixpkgs_dependencies")
rules_nixpkgs_dependencies()

load("@io_tweag_rules_nixpkgs//nixpkgs:nixpkgs.bzl", "nixpkgs_git_repository", "nixpkgs_package", "nixpkgs_python_configure")
nixpkgs_git_repository(
    name = "nixpkgs",
    remote = "https://github.com/NixOS/nixpkgs",
    revision = "18.09",
    sha256 = "6451af4083485e13daa427f745cbf859bc23cb8b70454c017887c006a13bd65e",
)
nixpkgs_python_configure(
    python3_attribute_path = "python37",
    repository = "@nixpkgs",
)

#_py_configure = """
#if [[ "$OSTYPE" == "darwin"* ]]; then
    #./configure --prefix=$(pwd)/bazel_install --with-openssl=$(brew --prefix openssl)
#else
    #./configure --prefix=$(pwd)/bazel_install
#fi
#"""

## NOTE: you need to have the SSL headers installed to build with openssl support (and use HTTPS).
## E.g. on Ubuntu: `sudo apt install libssl-dev`
#http_archive(
    #name = "python_interpreter",
    #build_file_content = """
#exports_files(["python_bin"])
#filegroup(
    #name = "files",
    #srcs = glob(["bazel_install/**"], exclude = ["**/* *"]),
    #visibility = ["//visibility:public"],
#)
#""",
    #patch_cmds = [
        #"mkdir $(pwd)/bazel_install",
        #_py_configure,
        #"make",
        #"make install",
        #"ln -s bazel_install/bin/python3 python_bin",
    #],
    #sha256 = "91923007b05005b5f9bd46f3b9172248aea5abc1543e8a636d59e629c3331b01",
    #strip_prefix = "Python-3.7.9",
    #urls = ["https://www.python.org/ftp/python/3.7.9/Python-3.7.9.tar.xz"],
#)

## Optional:
## Register the toolchain with the same python interpreter we used for pip in pip_install().
#register_toolchains("//:my_py_toolchain")
## End of in-build Python interpreter setup.

http_archive(
    name = "rules_python",
    url = "https://github.com/bazelbuild/rules_python/releases/download/0.1.0/rules_python-0.1.0.tar.gz",
    sha256 = "b6d46438523a3ec0f3cead544190ee13223a52f6a6765a29eae7b7cc24cc83a0",
)
load("@rules_python//python:pip.bzl", "pip_install")

pip_install(
    name = "py_deps",
    requirements = "//:requirements.txt",
    #python_interpreter_target = "@python_interpreter//:python_bin"
)
