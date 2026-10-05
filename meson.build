project(
  'uWebSockets',
  'cpp',
  version : '20.74.0',
  license : 'Apache-2.0',
  meson_version : '>= 1.3.0',
  default_options : ['cpp_std=c++20', 'buildtype=release', 'warning_level=1'],
)

uws_args = []
uws_deps = [dependency('usockets', default_options : ['ssl=' + get_option('ssl')])]

if get_option('zlib')
  uws_deps += dependency('zlib')
else
  uws_args += '-DUWS_NO_ZLIB'
endif

if get_option('proxy')
  uws_args += '-DUWS_WITH_PROXY'
endif

uws_inc = include_directories('src')

uwebsockets_dep = declare_dependency(
  include_directories : uws_inc,
  compile_args : uws_args,
  dependencies : uws_deps + [dependency('threads')],
)
meson.override_dependency('uwebsockets', uwebsockets_dep)

install_subdir('src', install_dir : get_option('includedir') / 'uWebSockets', strip_directory : true)

if get_option('examples')
  examples = [
    'Broadcast',
    'BroadcastingEchoServer',
    'Crc32',
    'EchoBody',
    'EchoServer',
    'HelloWorld',
    'HelloWorldThreaded',
    'HttpCache',
    'ParameterRoutes',
    'Precompress',
    'ServerName',
    'UpgradeAsync',
    'UpgradeSync',
  ]
  foreach example : examples
    executable(example, 'examples/' + example + '.cpp', dependencies : uwebsockets_dep)
  endforeach
endif
