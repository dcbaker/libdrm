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

amdgpu_files = files(
  'amdgpu_asic_id.h',
  'amdgpu_bo.c',
  'amdgpu_cs.c',
  'amdgpu_device.c',
  'amdgpu_gpu_info.c',
  'amdgpu_internal.h',
  'amdgpu_vamgr.c',
  'util_hash.c',
  'util_hash.h',
  'util_hash_table.c',
  'util_hash_table.h',
)

libdrm_amdgpu = shared_library(
  'drm_amdgpu',
  amdgpu_files,
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
  dependencies : pthreadstubs_dep,
  version : '1.0.0',
  install : true,
)

install_headers('amdgpu.h', subdir : 'libdrm')

pkg.generate(
  name : 'libdrm_amdgpu',
  description : 'Userspace interface to kernel DRM services for amdgpu',
  version : meson.project_version(),
  subdirs : ['', 'libdrm'],
  libraries : [libdrm_amdgpu],
  requires_private : 'libdrm',
)

test('amdgpu-symbol-check', find_program('amdgpu-symbol-check'))
