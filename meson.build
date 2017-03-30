# Copyright © 2017 Intel Corporation

# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:

# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.

# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

project('libdrm', 'c', version : '2.4.76-dev', default_options : ['-std=gnu99'])

pkg = import('pkgconfig')

conf_data = configuration_data()

global_warn_flags = []

atomic_dep = []
cunit_dep = []
pciaccess_dep = []
valgrind_dep = []
pthreadstubs_dep = dependency('pthread-stubs')  # TODO: is this always required?
cairo_dep = dependency('cairo', required : false)
if cairo_dep.found()
  conf_data.set('HAVE_CAIRO', true)
endif
thread_dep = dependency('threads')

system = host_machine.system()
if system.startswith('linux')
  add_project_arguments('-D_GNU_SOURCE', language : 'c')
endif

cc = meson.get_compiler('c')

# TODO: resolve whether we need -lrt
cc.find_library('m')
if cc.has_header('sys/sysctl.h')
  conf_data.set('HAVE_SYS_SYSCTL_H', true)
endif
if cc.has_header('sys/select.h')
  conf_data.set('HAVE_SYS_SELECT_H', true)
endif
if cc.has_header('alloca.h')
  conf_data.set('HAVE_ALLOCA_H', true)
endif
if cc.has_function('major', prefix : '#include <sys/sysmacros.h>')
  conf_data.set('MAJOR_IN_SYSMACROS', true)
elif cc.has_function('major', prefix : '#include <sys/mkdev.h>')
  conf_data.set('MAJOR_IN_MKDEV', true)
endif
if cc.has_function('open_memstream')
  conf_data.set('HAVE_OPEN_MEMSTREAM', true)
endif

if cc.compiles('''int foo_hidden(void) __attribute__((visibility("hidden")));''')
  conf_data.set('HAVE_ATTRIBUTE_VISIBILITY', true)
endif

# TODO: copy comment from configure.ac
global_warn_flag_opts = [
  '-Wall', '-Wextra', '-Wsign-compare',
  '-Werror-implicit-function-declaration', '-Wpointer-arith',
  '-Wwrite-strings', '-Wstrict-prototypes', '-Wmissing-prototypes',
  '-Wmissing-format-attribute', '-Wnested-externs', '-Wpacked',
  '-Wswitch-enum', '-Wmissing-format-attribute', '-Wstrict-aliasing=2',
  '-Winit-self', '-Wdeclaration-after-statement', '-Wold-style-definition',
  '-Wno-unused-parameter', '-Wno-attributes', '-Wno-long-long', '-Winline',
  '-Wshadow', '-Wno-missing-field-initializers',
]
foreach f : global_warn_flag_opts
  if cc.has_argument(f)
    global_warn_flags += f
  endif
endforeach

# Check for atomic intrinsics
if cc.compiles('''
	int atomic_add(int *i) { return __sync_add_and_fetch (i, 1); }
	int atomic_cmpxchg(int *i, int j, int k) { return __sync_val_compare_and_swap (i, j, k); }
    ''')
  conf_data.set('HAVE_LIBDRM_ATOMIC_PRIMITIVES', true)
elif (system.startswith('solaris') or system.startswith('netbsd')
      and cc.has_function('atomic_cas_uint'))
  if not cc.has_header('sys/atomic.h')
    error('wat?')
  endif
else
  atomic_dep = dependency('atomic_ops')
  conf_data.set('HAVE_LIB_ATOMIC_OPS', true)
endif

if get_option('udev') == 'yes'
  dependency('udev')
  conf_data.set('UDEV', true)
endif

cpu = host_machine.cpu_family()
if get_option('intel') != 'no'
  if cpu == 'x86' or cpu == 'x86_64'
    pciaccess_dep = dependency('pciaccess', version : '>=0.10')
    conf_data.set('HAVE_INTEL', true)
  endif
endif
if get_option('radeon') != 'no'
  conf_data.set('HAVE_RADEON', true)
endif
if get_option('amdgpu') != 'no'
  conf_data.set('HAVE_AMDGPU', true)
  cunit_dep = dependency('cunit', version : '>=2.1', required : false)
  if cunit_dep.found()
    conf_data.set('HAVE_CUNIT', true)
  endif
endif
if get_option('nouveau') != 'no'
  conf_data.set('HAVE_NOUVEAU', true)
  dl_lib = cc.find_library('dl')
  if dl_lib.found()
    dl_dep = declare_dependency(link_args : '-ldl')
  else
    error('nouveau tests require dlopen')
  endif
endif
if get_option('freedreno') != 'no'
  if cpu == 'arm'
    conf_data.set('HAVE_FREEDRENO', true)
    if get_option('freedreno-kgsl') == 'yes'
      conf_data.set('HAVE_FREEDRENO_KGSL', true)
    endif
  endif
endif
if get_option('vc4') != 'no'
  if cpu == 'arm'
    conf_data.set('HAVE_VC4', true)
  endif
endif
if get_option('vmwgfx') == 'yes'
  conf_data.set('HAVE_VMWGFX', true)
endif
if get_option('omap-experimental-api') == 'yes'
  if cpu == 'arm'
    conf_data.set('HAVE_OMAP', true)
  endif
endif
if get_option('exynos-experimental-api') == 'yes'
  if cpu == 'arm'
    conf_data.set('HAVE_EXYNOS', true)
  endif
endif
if get_option('tegra-experimental-api') == 'yes'
  if cpu == 'arm'
    conf_data.set('HAVE_TEGRA', true)
  endif
endif
if get_option('etnaviv-experimental-api') == 'yes'
  if cpu == 'arm'
    conf_data.set('HAVE_ETNAVIV', true)
  endif
endif

if get_option('libkms') == 'auto'
  if (system.startswith('linux') or
      system.startswith('freebsd') or
      system.startswith('dragonfly') or
      (system.startswith('kfreebsd') and system.endswith('-gnu')))
    conf_data.set('HAVE_LIBKMS', true)
  elif get_option('libkms') == 'no'
    conf_data.set('HAVE_LIBKMS', false)
  endif
elif get_option('libkms') == 'yes'
  conf_data.set('HAVE_LIBKMS', true)
else
  conf_data.set('HAVE_LIBKMS', false)
endif

# TODO: https://github.com/mesonbuild/meson/issues/826
# This only works with a dev build of meson
if get_option('valgrind') != 'no'
  valgrind_dep = dependency(
    'valgrind',
    headers_only : true,
    required : get_option('valgrind') == 'yes'
  )
  if valgrind_dep.found()
    conf_data.set('HAVE_VALGRIND', true)
  endif
endif

config_h = configure_file(
  input : 'meson_config.h.in',
  output : 'config.h',
  configuration : conf_data,
)
add_project_arguments('-DHAVE_CONFIG_H', language : 'c')

libdrm_files = files(
  'xf86drm.c',
  'xf86drmHash.c',
  'xf86drmHash.h',
  'xf86drmRandom.c',
  'xf86drmRandom.h',
  'xf86drmSL.c',
  'xf86drmMode.c',
  'xf86atomic.h',
  'libdrm_macros.h',
  'libdrm_lists.h',
  'util_double_list.h',
  'util_math.h',
)

drm_include = include_directories('include/drm')
base_include = include_directories('.')

libdrm = shared_library(
  'drm',
  libdrm_files,
  include_directories : [base_include, drm_include],
  dependencies : valgrind_dep,
  c_args : global_warn_flags,
  link_args : '-lm',
  version : '2.4.0',
  install : true,
)

install_headers(
  'libsync.h',
  'xf86drm.h',
  'xf86drmMode.h',
)

pkg.generate(
  name : 'libdrm',
  filebase : 'libdrm',
  description : 'Userspace interface to kernel DRM services',
  version : meson.project_version(),
  libraries : [libdrm],
  subdirs : ['', 'libdrm'],
)

subdir('include/drm')
if conf_data.get('HAVE_LIBKMS', false)
  subdir('libkms')
endif
if conf_data.get('HAVE_INTEL', false)
  subdir('intel')
endif
if conf_data.get('HAVE_NOUVEAU', false)
  subdir('nouveau')
endif
if conf_data.get('HAVE_RADEON', false)
  subdir('radeon')
endif
if conf_data.get('HAVE_AMDGPU', false)
  subdir('amdgpu')
endif
if conf_data.get('HAVE_OMAP', false)
  subdir('omap')
endif
if conf_data.get('HAVE_EXYNOS', false)
  subdir('exynos')
endif
if conf_data.get('HAVE_FREEDRENO', false)
  subdir('freedreno')
endif
if conf_data.get('HAVE_TEGRA', false)
  subdir('tegra')
endif
if conf_data.get('HAVE_VC4', false)
  subdir('vc4')
endif
if conf_data.get('HAVE_ETNAVIV', false)
  subdir('etnaviv')
endif
subdir('tests')
if get_option('manpages')
  subdir('man')
endif

libdrm_dep = declare_dependency(
  link_with : libdrm,
  include_directories : include_directories('include/drm')
)
