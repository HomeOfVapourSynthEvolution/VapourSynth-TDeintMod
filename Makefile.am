warning_flags = -Wall -Wextra -Wshadow -Wno-unused-parameter -Wno-attributes
common_cflags = -O3 -ffast-math -fvisibility=hidden $(warning_flags) $(MFLAGS)
AM_CXXFLAGS = -std=c++14 $(common_cflags)

AM_CPPFLAGS = $(VapourSynth_CFLAGS)

lib_LTLIBRARIES = libtdeintmod.la

libtdeintmod_la_SOURCES = TDeintMod/TDeintMod.cpp \
                          TDeintMod/TDeintMod.hpp \
                          TDeintMod/vectorclass/instrset.h \
                          TDeintMod/vectorclass/instrset_detect.cpp

if VS_TARGET_CPU_X86
libtdeintmod_la_SOURCES += TDeintMod/TDeintMod_SSE2.cpp \
                           TDeintMod/vectorclass/vectorclass.h \
                           TDeintMod/vectorclass/vectorf128.h \
                           TDeintMod/vectorclass/vectorf256.h \
                           TDeintMod/vectorclass/vectorf256e.h \
                           TDeintMod/vectorclass/vectori128.h \
                           TDeintMod/vectorclass/vectori256.h \
                           TDeintMod/vectorclass/vectori256e.h

noinst_LTLIBRARIES = libavx2.la

libavx2_la_SOURCES = TDeintMod/TDeintMod_AVX2.cpp
libavx2_la_CXXFLAGS = $(AM_CXXFLAGS) -mavx2 -mfma

libtdeintmod_la_LIBADD = libavx2.la
endif

libtdeintmod_la_LDFLAGS = -no-undefined -avoid-version $(PLUGINLDFLAGS)
