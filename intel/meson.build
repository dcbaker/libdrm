# Copyright © 2017-2018 Intel Corporation

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

libdrm_intel = shared_library(
  'drm_intel',
  [
    files(
      'intel_bufmgr.c', 'intel_bufmgr_fake.c', 'intel_bufmgr_gem.c',
      'intel_decode.c', 'mm.c',
    ),
    config_file,
  ],
  include_directories : [inc_root, inc_drm],
  link_with : libdrm,
  dependencies : [dep_pciaccess, dep_pthread_stubs, dep_rt, dep_valgrind],
  c_args : warn_c_args,
  version : '1.0.0',
  install : true,
)

ext_libdrm_intel = declare_dependency(
  link_with : [libdrm, libdrm_intel],
  include_directories : [inc_drm, include_directories('.')],
)

install_headers(
  'intel_bufmgr.h', 'intel_aub.h', 'intel_debug.h',
  subdir : 'libdrm',
)

pkg.generate(
  name : 'libdrm_intel',
  libraries : libdrm_intel,
  subdirs : ['.', 'libdrm'],
  version : meson.project_version(),
  requires : 'libdrm',
  description : 'Userspace interface to intel kernel DRM services',
)

test_decode = executable(
  'test_decode',
  files('test_decode.c'),
  include_directories : [inc_root, inc_drm],
  link_with : [libdrm, libdrm_intel],
  c_args : warn_c_args,
)

test(
  'gen4-3d.batch',
  prog_bash,
  args : files('tests/gen4-3d.batch.sh'),
  workdir : meson.current_build_dir(),
)
test(
  'gen45-3d.batch',
  prog_bash,
  args : files('tests/gm45-3d.batch.sh'),
  workdir : meson.current_build_dir(),
)
test(
  'gen5-3d.batch',
  prog_bash,
  args : files('tests/gen5-3d.batch.sh'),
  workdir : meson.current_build_dir(),
)
test(
  'gen6-3d.batch',
  prog_bash,
  args : files('tests/gen6-3d.batch.sh'),
  workdir : meson.current_build_dir(),
)
test(
  'gen7-3d.batch',
  prog_bash,
  args : files('tests/gen7-3d.batch.sh'),
  workdir : meson.current_build_dir(),
)
test(
  'gen7-2d-copy.batch',
  prog_bash,
  args : files('tests/gen7-2d-copy.batch.sh'),
  workdir : meson.current_build_dir(),
)
test(
  'intel-symbol-check',
  prog_bash,
  args : [files('intel-symbol-check'), libdrm_intel]
)