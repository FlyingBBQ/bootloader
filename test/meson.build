# add your test sources here
test_src = files('test_main.cpp')

# find external programs from path (OS independant)
coverage = find_program('gcovr', required : get_option('enable_coverage'))

if not coverage.found()
  warning('gcovr not found, cannot generate coverage report')
  cov_args = []
  cov_link_args = []
else
  cov_args = ['-ftest-coverage', '-fprofile-arcs']
  cov_link_args = ['-lgcov']
endif

# compile the test executable
# native: use the native compiler instead of cross-compiler
test_exe = executable(
  'test_exe',
  [test_src, 'doctest_main.cpp'],
  c_args : [c_args, cov_args],
  cpp_args : [cpp_args, cov_args],
  link_args : [cov_link_args],
  dependencies : doctest_dep,
  include_directories : test_inc,
  native : true)

# make the test executable visible to the build system test framework
test('Unit tests', test_exe)

# custom target to run gcovr
if coverage.found()
  run_target('covr',
    command : [coverage, meson.build_root(), '-r', meson.source_root() + '/src', '-e', 'doctest.h'],
    depends : test_exe)
endif
