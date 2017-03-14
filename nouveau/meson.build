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

nouveau_files = files(
  'nouveau.c',
  'pushbuf.c',
  'bufctx.c',
  'abi16.c',
  'private.h',
)

nouveau_include = include_directories('.')

libdrm_nouveau = shared_library(
  'drm_nouveau',
  nouveau_files,
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
  dependencies : pthreadstubs_dep,
  version : '2.0.0',
  install : true,
)

install_headers('nouveau.h', subdir : 'libdrm/nouveau')
install_headers(
  'nvif/class.h',
  'nvif/cl0080.h',
  'nvif/cl9097.h',
  'nvif/if0002.h',
  'nvif/if0003.h',
  'nvif/ioctl.h',
  'nvif/unpack.h',
  subdir : 'nouveau/nvif',
)

pkg.generate(
  name : 'libdrm_nouveau',
  description : 'Userspace interface to nouveau kernel DRM services',
  version : meson.project_version(),
  subdirs : ['', 'libdrm'],
  libraries : [libdrm_nouveau],
  requires_private : 'libdrm',
)

test('nouveau-symbol-check', find_program('nouveau-symbol-check'))
