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

xsltproc = find_program('xsltproc')
sed = find_program('sed')

stylesheet_url = 'http://docbook.sourceforge.net/release/xsl/current/manpages/docbook.xsl'
ret = run_command(xsltproc, '--nonet', stylesheet_url)
if ret.returncode() != 0
  error('Cannot build man pages without docbook-xml')
endif

xsltproc_args = [xsltproc, '-o', '@OUTPUT@',
                 '--stringparam', 'man.authors.section.enabled', '0',
                 '--stringparam', 'man.copyright.section.enabled', '0',
                 '--stringparam', 'funcsynopsis.style', 'ansi',
                 '--stringparam', 'man.output.quietly', '1',
                 '--noout', stylesheet_url, '@INPUT@']

# TODO: https://github.com/mesonbuild/meson/issues/1364
# This issue is about creating reusable custom_target templates, which would
# simplify the following custom_targets considerably.
drm_avail_man = custom_target(
  'drmAvailable.3',
  input : 'drmAvailable.xml',
  output : '@BASENAME@.3',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man3',
)

drm_handleevent_man = custom_target(
  'drmHandleEvent.3',
  input : 'drmHandleEvent.xml',
  output : '@BASENAME@.3',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man3',
)

drm_modegetresources_man = custom_target(
  'drmModeGetResources.3',
  input : 'drmModeGetResources.xml',
  output : '@BASENAME@.3',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man3',
)

drm_man = custom_target(
  'drm.7',
  input : 'drm.xml',
  output : '@BASENAME@.7',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man7',
)

drm_kms_man = custom_target(
  'kms.7',
  input : 'drm-kms.xml',
  output : '@BASENAME@.7',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man7',
)

drm_memory_man = custom_target(
  'memory.7',
  input : 'drm-memory.xml',
  output : '@BASENAME@.7',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man7',
)

drm_mm = custom_target(
  'mm.7',
  input : 'drm-memory.xml',
  output : 'drm-mm.7',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man7',
)

drm_gem = custom_target(
  'gem.7',
  input : 'drm-memory.xml',
  output : 'drm-gem.7',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man7',
)

drm_gem = custom_target(
  'ttm.7',
  input : 'drm-memory.xml',
  output : 'drm-ttm.7',
  command : xsltproc_args,
  install : true,
  install_dir : 'usr/share/man/man7',
)
