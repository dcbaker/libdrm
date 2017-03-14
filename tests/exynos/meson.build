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

test_exynos_fimg2d_perf = executable(
  'exynos_fimg2d_perf',
  'exynos_fim2d_perf.c',
  include_directories : [base_include, libkms_include, exynos_include, drm_include],
  link_with : [libdrm, libdrm_exynos],
)

test_exynos_fimg2d_event = executable(
  'exynos_fimg2d_event',
  'exynos_fimg2d_event.c',
  include_directories : [base_include, kms_include, exynos_include, drm_include],
  link_with : [libdrm, libdrm_exynos],
)

if conf_data.get('HAVE_LIBKMS', false):
  test_exynos_fimg2d_test = executable(
    'exynos_fimg2d_test',
    'exynos_fimg2d_test.c',
    dependencies : test_util_dep,
    include_directories : [base_include, kms_include, exynos_include, drm_include],
    link_with : [libdrm, libdrm_exynos],
  )
endif
