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

libkms_files = files(
  'internal.h',
  'linux.c',
  'dumb.c',
  'api.c',
)

libkms_include = include_directories('.')

if conf_data.get('HAVE_VMWGFX', false)
  libkms_files += files('vmwgfx.c')
endif

if conf_data.get('HAVE_INTEL', false)
  libkms_files += files('intel.c')
endif

if conf_data.get('HAVE_NOUVEAU', false)
  libkms_files += files('nouveau.c')
endif

if conf_data.get('HAVE_RADEON', false)
  libkms_files += files('radeon.c')
endif

if conf_data.get('HAVE_EXYNOS', false)
  libkms_files += files('exynos.c')
endif

libkms = shared_library(
  'kms',
  libkms_files,
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include, include_directories('../exynos')],
  link_with : libdrm,
  version : '1.0.0',
  install : true,
)

install_headers('libkms.h', subdir : 'libkms')

pkg.generate(
  name : 'libkms',
  description : 'Library that abstracts away the different mm interfaces for kernel drivers',
  version : '1.0.0',
  requires_private : 'libdrm',
  subdirs : ['libkms'],
  libraries : [libkms],
)

test('kms-symbol-check', find_program('kms-symbol-check'))
