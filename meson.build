project('flann', [ 'c', 'cpp' ],
        default_options : ['c_std=c11', 'cpp_std=c++14'],
        license: 'BSD')

version = '1.9.1'

compiler = meson.get_compiler('cpp')

conf_data = configuration_data()

version_pretty = version
conf_data.set('flann_version', version)
configure_file(input : 'src/cpp/flann/config.meson',
               output : 'config.h',
               configuration : conf_data)

inc = include_directories('src/cpp')
defines = [ '-D_FLANN_VERSION="' + version + '"']

if get_option('default_library') == 'shared'
    defines += [ '-DFLANN_EXPORTS' ]
endif
if compiler.get_define('_WIN32') != ''
    defines += [ '-DWIN32' ]
endif

cpp_src = [
    'src/cpp/flann/flann_cpp.cpp',
    'src/cpp/flann/ext/lz4.c',
    'src/cpp/flann/ext/lz4hc.c'
]

c_src = [
    'src/cpp/flann/flann.cpp',
    'src/cpp/flann/ext/lz4.c',
    'src/cpp/flann/ext/lz4hc.c'
]

cpp_lib = library('flann_cpp', cpp_src,
        version: version,
        c_args: defines,
        cpp_args: defines,
        include_directories: inc)
cpp_dep = declare_dependency(link_with: cpp_lib,
        include_directories: inc)

c_lib = library('flann', c_src,
        version: version,
        c_args: defines,
        c_args: defines,
        include_directories: inc)
c_dep = declare_dependency(link_with: c_lib,
        include_directories: inc)
