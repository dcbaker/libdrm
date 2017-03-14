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

freedreno_files = files(
  'freedreno_device.c',
  'freedreno_pipe.c',
  'freedreno_priv.h',
  'freedreno_ringbuffer.c',
  'freedreno_bo.c',
  'freedreno_bo_cache.c',
  'msm/msm_bo.c',
  'msm/msm_device.c',
  'msm/msm_drm.h',
  'msm/msm_pipe.c',
  'msm/msm_priv.h',
  'msm/msm_ringbuffer.c',
)

if get_option('freedreno-kgsl') == 'yes'
  freedreno_kgsl_files = files(
    'kgsl/kgsl_bo.c',
    'kgsl/kgsl_device.c',
    'kgsl/kgsl_drm.h',
    'kgsl/kgsl_pipe.c',
    'kgsl/kgsl_priv.h',
    'kgsl/kgsl_ringbuffer.c',
    'kgsl/msm_kgsl.h',
  )
else
  freedreno_kgsl_files = []
endif

libdrm_freedreno = shared_library(
  'drm_freedreno',
  [freedreno_files, freedreno_kgsl_files],
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
  dependencies : pthreadstubs_dep,
  version : '1.0.0',
  install : true,
)

install_headers('freedreno_drmif.h', 'freedreno_ringbuffer.h', subdir : 'freedreno')

pkg.generate(
  name : 'libdrm_freedreno',
  description : 'Userspace interface to freedreno kernel DRM services',
  version : meson.project_version(),
  subdirs : ['', 'libdrm', 'freedreno'],
  libraries : [libdrm_freedreno],
  requires_private : 'libdrm',
)

test('freedreno-symbol-check', find_program('freedreno-symbol-check'))
