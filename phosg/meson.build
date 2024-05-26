# It seems that on some Linux variants (e.g. Raspbian) we also need -latomic,
# but this library does not exist on others (e.g. Ubuntu) nor on macOS

phosg_dependencies = [
    cpp.find_library('pthread', required: true),
    cpp.find_library('z', required: true),
]

if (
    host_machine.system() == 'linux'
    and host_machine.cpu_family() in ['aarch64', 'arm']
)
    latomic = cpp.find_library('atomic', required: true)
    phosg_dependencies += [latomic]
endif

phosg_lib = library(
    'phosg',
    'Arguments.cc',
    'Encoding.cc',
    'Filesystem.cc',
    'Hash.cc',
    'Image.cc',
    'JSON.cc',
    'Network.cc',
    'Process.cc',
    'Random.cc',
    'Strings.cc',
    'Time.cc',
    'Tools.cc',
    'UnitTest.cc',
    dependencies: phosg_dependencies,
    install: true,
)

install_headers(
    'Arguments.hh',
    'Containers.hh',
    'Encoding.hh',
    'Filesystem.hh',
    'Hash.hh',
    'Image.hh',
    'ImageTextFont.hh',
    'JSON.hh',
    'KDTree-inl.hh',
    'KDTree.hh',
    'LRUMap.hh',
    'LRUSet-inl.hh',
    'LRUSet.hh',
    'Math.hh',
    'Network.hh',
    'Platform.hh',
    'Process.hh',
    'Random.hh',
    'Strings.hh',
    'Time.hh',
    'Tools.hh',
    'Types.hh',
    'UnitTest.hh',
    'Vector-inl.hh',
    'Vector.hh',
    subdir: 'phosg',
)

phosg_dep = declare_dependency(
    include_directories: root_inc,
    link_with: [phosg_lib],
)

bindiff_exe = executable(
    'bindiff',
    'BinDiff.cc',
    dependencies: [phosg_dep],
    install: true,
)
jsonformat_exe = executable(
    'jsonformat',
    'JSONFormat.cc',
    dependencies: [phosg_dep],
    install: true,
)
parse_data_exe = executable(
    'parse-data',
    'ParseData.cc',
    dependencies: [phosg_dep],
    install: true,
)
phosg_png_conv_exe = executable(
    'phosg-png-conv',
    'PhosgPNGConv.cc',
    dependencies: [phosg_dep],
    install: true,
)

foreach test_name : [
    'ArgumentsTest',
    'EncodingTest',
    'FilesystemTest',
    'HashTest',
    'ImageTest',
    'JSONTest',
    'KDTreeTest',
    'LRUMapTest',
    'LRUSetTest',
    'ProcessTest',
    'StringsTest',
    'TimeTest',
    'UnitTestTest',
    'ToolsTest',
]
    test_exe = executable(
        test_name,
        f'@test_name@.cc',
        dependencies: [phosg_dep],
    )
    test(test_name, test_exe)

endforeach

