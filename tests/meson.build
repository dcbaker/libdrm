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

test_drmsl = executable(
  'drmsl',
  'drmsl.c',
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
)

test_hash = executable(
  'hash',
  'hash.c',
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
)

test_random = executable(
  'random',
  'random.c',
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
)

test_drmdevice = executable(
  'drmdevice',
  'drmdevice.c',
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include],
  link_with : libdrm,
)

test('drmsl', test_drmsl)
test('hash', test_hash)
# XXX: This test never seems to finish
#test('random', test_random)
test('drmdevice', test_drmdevice)

test_include = include_directories('.')

subdir('util')
subdir('kms')
subdir('modeprint')
subdir('proptest')
subdir('modetest')
subdir('vbltest')
if conf_data.get('HAVE_LIBKMS', false)
  subdir('kmstest')
endif
if conf_data.get('HAVE_RADEON', false)
  subdir('radeon')
endif
if conf_data.get('HAVE_AMDGPU', false) and conf_data.get('HAVE_CUNIT', false)
  subdir('amdgpu')
endif
if conf_data.get('have_exynos', false)
  subdir('exynos')
endif
if conf_data.get('HAVE_TEGRA', false)
  subdir('tegra')
endif
if conf_data.get('HAVE_ETNAVIV', false)
  subdir('etnaviv')
endif
if conf_data.get('HAVE_NOUVEAU', false)
  subdir('nouveau')
endif
