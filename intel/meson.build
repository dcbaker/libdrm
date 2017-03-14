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

libdrm_intel_files = files(
  'intel_bufmgr.c',
  'intel_bufmgr_priv.h',
  'intel_bufmgr_fake.c',
  'intel_bufmgr_gem.c',
  'intel_decode.c',
  'intel_chipset.h',
  'mm.c',
  'mm.h',
  'uthash.h',
)

libdrm_intel = shared_library(
  'drm_intel',
  libdrm_intel_files,
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
  dependencies : [pthreadstubs_dep, pciaccess_dep, valgrind_dep],
  version : '1.0.0',
  install : true,
)

install_headers('intel_bufmgr.h', 'intel_aub.h', 'intel_debug.h', subdir : 'libdrm')

pkg.generate(
  name : 'libdrm_intel',
  description : 'Userspace interface to intel kernel DRM services',
  version : meson.project_version(),
  requires : 'libdrm',
  subdirs : ['', 'libdrm'],
  libraries : [libdrm_intel],
)

test('intel-symbol-check', find_program('intel-symbol-check'))
