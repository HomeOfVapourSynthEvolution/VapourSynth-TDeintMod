project('TDeintMod', 'cpp',
  default_options : ['buildtype=release', 'b_ndebug=if-release', 'cpp_std=c++14'],
  meson_version : '>=0.48.0',
  version : '10'
)

add_project_arguments('-ffast-math', language : 'cpp')

sources = [
  'TDeintMod/TDeintMod.cpp',
  'TDeintMod/TDeintMod.hpp',
  'TDeintMod/vectorclass/instrset.h',
  'TDeintMod/vectorclass/instrset_detect.cpp'
]

vapoursynth_dep = dependency('vapoursynth').partial_dependency(compile_args : true, includes : true)

libs = []

if host_machine.cpu_family().startswith('x86')
  add_project_arguments('-DVS_TARGET_CPU_X86', '-mfpmath=sse', '-msse2', language : 'cpp')

  sources += [
    'TDeintMod/TDeintMod_SSE2.cpp',
    'TDeintMod/vectorclass/vectorclass.h',
    'TDeintMod/vectorclass/vectorf128.h',
    'TDeintMod/vectorclass/vectorf256.h',
    'TDeintMod/vectorclass/vectorf256e.h',
    'TDeintMod/vectorclass/vectori128.h',
    'TDeintMod/vectorclass/vectori256.h',
    'TDeintMod/vectorclass/vectori256e.h'
  ]

  libs += static_library('avx2', 'TDeintMod/TDeintMod_AVX2.cpp',
    dependencies : vapoursynth_dep,
    cpp_args : ['-mavx2', '-mfma'],
    gnu_symbol_visibility : 'hidden'
  )
endif

shared_module('tdeintmod', sources,
  dependencies : vapoursynth_dep,
  link_with : libs,
  install : true,
  install_dir : join_paths(vapoursynth_dep.get_pkgconfig_variable('libdir'), 'vapoursynth'),
  gnu_symbol_visibility : 'hidden'
)
