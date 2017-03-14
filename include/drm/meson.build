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

install_headers(
  'drm.h',
  'drm_fourcc.h',
  'drm_mode.h',
  'drm_sarea.h',
  'i915_drm.h',
  'mach64_drm.h',
  'mga_drm.h',
  'nouveau_drm.h',
  'qxl_drm.h',
  'r128_drm.h',
  'radeon_drm.h',
  'amdgpu_drm.h',
  'savage_drm.h',
  'sis_drm.h',
  'tegra_drm.h',
  'vc4_drm.h',
  'via_drm.h',
  'virtgpu_drm.h',
  subdir : 'libdrm',
)

if conf_data.get('HAVE_VMWGFX')
  install_headers(
    'vmwgfx_drm.h',
    subdir : 'libdrm',
  )
endif
