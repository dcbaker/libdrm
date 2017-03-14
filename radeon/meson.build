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

radeon_files = files(
  'radeon_bo_gem.c',
  'radeon_cs_gem.c',
  'radeon_cs_space.c',
  'radeon_bo.c',
  'radeon_cs.c',
  'radeon_surface.c',
)

libdrm_radeon = shared_library(
  'drm_radeon',
  radeon_files,
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
  dependencies : pthreadstubs_dep,
  version : '1.0.1',
  install : true,
)

install_headers(
  'radeon_bo.h',
  'radeon_cs.h',
  'radeon_surface.h',
  'radeon_bo_gem.h',
  'radeon_cs_gem.h',
  'radeon_bo_int.h',
  'radeon_cs_int.h',
  'r600_pci_ids.h',
  subdir : 'libdrm'
)

pkg.generate(
  name : 'libdrm_radeon',
  description : 'Userspace interface to kernel DRM services for radeon',
  version : meson.project_version(),
  subdirs : ['', 'libdrm'],
  libraries : [libdrm_radeon],
  requires_private : 'libdrm',
)

test('radeon-symbol-check', find_program('radeon-symbol-check'))
