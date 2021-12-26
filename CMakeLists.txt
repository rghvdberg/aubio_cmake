# ISC License (ISC)

# Copyright 2021 Rob van den Berg <rghvdberg at gmail dot com>

# Permission to use, copy, modify, and/or distribute this software for any purpose
#  with or without fee is hereby granted, provided that the above copyright notice 
#  and this permission notice appear in all copies. THE SOFTWARE IS PROVIDED 
#  "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE 
#  INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT 
#  SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL 
#  DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, 
#  WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING 
#  OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

cmake_minimum_required(VERSION 3.0.0)

file(READ "aubio/VERSION" ver)
string(REGEX MATCH "AUBIO_MAJOR_VERSION=([0-9]*)" _ ${ver})
set(ver_major ${CMAKE_MATCH_1})
string(REGEX MATCH "AUBIO_MINOR_VERSION=([0-9]*)" _ ${ver})
set(ver_minor ${CMAKE_MATCH_1})
string(REGEX MATCH "AUBIO_PATCH_VERSION=([0-9]*)" _ ${ver})
set(ver_patch ${CMAKE_MATCH_1})

project(aubio VERSION ${ver_major}.${ver_minor}.${ver_patch})

option(HAVE_CONFIG_H "Have Config" ON)
option(HAVE_STDLIB_H "Have stdlib" ON)
option(HAVE_STDIO_H "Have stdio" ON)
option(HAVE_MATH_H "Have math.h" ON)
option(HAVE_STRING_H "Have string.h" ON)
option(HAVE_LIMITS_H "Have limits.h" ON)
option(HAVE_STDARG_H "Have stdarg.h" ON)
option(HAVE_GETOPT_H "Have getopt.h" ON)
option(HAVE_UNISTD_H "Have unistd.h" ON)
option(HAVE_C99_VARARGS_MACROS "Have c99 varargs macros" ON)
option(HAVE_WAVREAD "Have wavread" ON)
option(HAVE_WAVWRITE "Have wavwrite" ON)
option(HAVE_MEMCPY_HACKS "Have memcpy hacks" ON)
option(HAVE_ERRNO_H "Have errno.h" ON)

add_definitions(-DHAVE_CONFIG_H)

configure_file(AubioConfig.h.in config.h)

add_library(
  aubio STATIC
  aubio/src/cvec.c
  aubio/src/fmat.c
  aubio/src/fvec.c
  aubio/src/lvec.c
  aubio/src/mathutils.c
  aubio/src/musicutils.c
  aubio/src/vecutils.c
  aubio/src/io/audio_unit.c
  aubio/src/io/ioutils.c
  aubio/src/io/sink.c
  aubio/src/io/sink_apple_audio.c
  aubio/src/io/sink_sndfile.c
  aubio/src/io/sink_wavwrite.c
  aubio/src/io/source.c
  aubio/src/io/source_apple_audio.c
  aubio/src/io/source_avcodec.c
  aubio/src/io/source_sndfile.c
  aubio/src/io/source_wavread.c
  aubio/src/io/utils_apple_audio.c
  aubio/src/notes/notes.c
  aubio/src/onset/onset.c
  aubio/src/onset/peakpicker.c
  aubio/src/pitch/pitch.c
  aubio/src/pitch/pitchfcomb.c
  aubio/src/pitch/pitchmcomb.c
  aubio/src/pitch/pitchschmitt.c
  aubio/src/pitch/pitchspecacf.c
  aubio/src/pitch/pitchyin.c
  aubio/src/pitch/pitchyinfast.c
  aubio/src/pitch/pitchyinfft.c
  aubio/src/spectral/dct_accelerate.c
  aubio/src/spectral/dct_fftw.c
  aubio/src/spectral/dct_ipp.c
  aubio/src/spectral/dct_ooura.c
  aubio/src/spectral/dct_plain.c
  aubio/src/spectral/fft.c
  aubio/src/spectral/filterbank.c
  aubio/src/spectral/filterbank_mel.c
  aubio/src/spectral/mfcc.c
  aubio/src/spectral/ooura_fft8g.c
  aubio/src/spectral/phasevoc.c
  aubio/src/spectral/specdesc.c
  aubio/src/spectral/statistics.c
  aubio/src/spectral/tss.c
  aubio/src/synth/sampler.c
  aubio/src/synth/wavetable.c
  aubio/src/tempo/beattracking.c
  aubio/src/tempo/tempo.c
  aubio/src/temporal/a_weighting.c
  aubio/src/temporal/biquad.c
  aubio/src/temporal/c_weighting.c
  aubio/src/temporal/filter.c
  aubio/src/temporal/resampler.c
  aubio/src/utils/hist.c
  aubio/src/utils/log.c
  aubio/src/utils/parameter.c
  aubio/src/utils/scale.c
  aubio/src/utils/windll.c)

target_include_directories(aubio PUBLIC "${PROJECT_BINARY_DIR}"
                                        "${PROJECT_SOURCE_DIR}/aubio/src")
