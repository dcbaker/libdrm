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

if conf_data.get('HAVE_LIBKMS', false)
  test_etnaviv_2d = executable(
    'etnaviv_2d_test',
    ['cmdstream.xml.h', 'etnaviv_2d_test.c', 'state.xml.h', 'state_2d.xml.h',
     'write_bmp.c', 'write_bmp.h'],
    c_args : global_warn_flags,
    include_directories : [base_include, drm_include, etnaviv_include],
    link_with : [libdrm, libdrm_etnaviv],
    dependencies : thread_dep
  )
endif

test_etnaviv_cmd_stream = executable(
  'etnaviv_cmd_stream_test',
  'etnaviv_cmd_stream_test.c',
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include, etnaviv_include],
  link_with : [libdrm_etnaviv],
  dependencies : thread_dep
)

test_etnaviv_bo_cache = executable(
  'etnaviv_bo_cache_test',
  'etnaviv_bo_cache_test.c',
  c_args : global_warn_flags,
  include_directories : [base_include, drm_include, etnaviv_include],
  link_with : [libdrm, libdrm_etnaviv],
  dependencies : thread_dep
)
