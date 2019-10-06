# general project settings
project('bootloader', 'c', 'cpp',
  version : '1.0',
  default_options : [
    'b_lto=false',
    #'b_asneeded=false',
    #'b_lundef=false',
    'b_pch=false',
    'b_staticpic=false',
    'c_std=c99',
    'cpp_std=c++11'
    ],
  meson_version : '>=0.51.0')

# global variables tracking sources and includes
c_args = ['-Wall', '-Werror', '-Wextra', '-pedantic']
cpp_args = ['-Wall', '-Werror', '-Wextra', '-pedantic']
c_link_args = []
cpp_link_args = []
project_src = []
project_inc = []
test_src = []
test_inc = []
defines = []

# include doxygen generation if enabled
if get_option('enable_docs')
  subdir('docs')
endif

# include the source files of the project
subdir('src')

# include tests if enabled
if get_option('enable_test')
  # clone the git repository and install it in the subprojects directory
  # the remote git url is specified in subprojects/doctest.wrap
  doctest_git = subproject('doctest')
  # get the doctest dependency from the subproject
  doctest_dep = doctest_git.get_variable('doctest_dep')
  # include the test directory
  subdir('test')
else
  # disable test globally and do not compile them
  defines += '-DDOCTEST_CONFIG_DISABLE'
endif

# add defines to the c_args
c_args += defines

# compile the main executable
main = executable('main',
  [project_src],
  #name_suffix : 'elf',
  c_args : [c_args],
  link_args : [c_link_args],
  include_directories : [project_inc])
