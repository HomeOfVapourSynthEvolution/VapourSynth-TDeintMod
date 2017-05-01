warning_flags = -Wall -Wextra -Wshadow -Wno-unused-parameter
common_cflags = -O3 -ffast-math $(MFLAGS) $(warning_flags)
AM_CXXFLAGS = -std=c++14 $(common_cflags)

AM_CPPFLAGS = $(VapourSynth_CFLAGS)

lib_LTLIBRARIES = libtdeintmod.la

libtdeintmod_la_SOURCES = TDeintMod/TDeintMod.cpp \
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

libavx2_la_CXXFLAGS = $(AM_CXXFLAGS) -mfma -mavx2


libtdeintmod_la_LIBADD = libavx2.la
endif

libtdeintmod_la_LDFLAGS = -no-undefined -avoid-version $(PLUGINLDFLAGS)
