project(
  'signals',
  'cpp',
  version: '26.11.0',
  meson_version: '>=1.12.0',
  default_options: {
    'cpp_std': 'c++26',
    'warning_level': '3',
  },
)

signals_library_sources = files(
  'source/connection.cpp',
  'source/scoped_connection.cpp',
)
signals_library_include_directories = include_directories('include')

signals_library = library(
  'signals',
  sources: signals_library_sources,
  include_directories: signals_library_include_directories,
  version: meson.project_version(),
  soversion: '1',
  install: true,
)

signals_library_dependency = declare_dependency(
  include_directories: signals_library_include_directories,
  link_with: signals_library,
)

meson.override_dependency(
  'signals',
  signals_library_dependency,
)


enable_tests = get_option('tests').enable_auto_if(meson.is_subproject() == false).enabled()
summary({'run tests': enable_tests}, bool_yn: true, section: 'Features')
if enable_tests == true
  test(
    'signals_test_suite',
    executable(
      'test_suite',
      build_by_default: false,
      dependencies: [signals_library_dependency],
      sources: ['testing/test_suite.cpp'],
    ),
  )
endif
