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

etnaviv_files = files(
  'etnaviv_device.c',
  'etnaviv_gpu.c',
  'etnaviv_bo.c',
  'etnaviv_bo_cache.c',
  'etnaviv_pipe.c',
  'etnaviv_cmd_stream.c',
  'etnaviv_drm.h',
  'etnaviv_priv.h',
)

etnaviv_include = include_directories('.')

libdrm_etnaviv = shared_library(
  'drm_etnaviv',
  etnaviv_files,
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
  dependencies : [pthreadstubs_dep, valgrind_dep],
  version : '1.0.0',
  install : true,
)

install_headers('etnaviv_drmif.h', subdir : 'libdrm')

pkg.generate(
  name : 'libdrm_etnaviv',
  description : 'Userspace interface to etnaviv kernel DRM services',
  version : meson.project_version(),
  subdirs : ['', 'libdrm'],
  libraries : [libdrm_etnaviv],
  requires_private : 'libdrm',
)

test('etnaviv-symbol-check', find_program('etnaviv-symbol-check'))
