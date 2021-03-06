include Makefile.mk

OBJS = \
	kiss_fft/kiss_fft.c.o \
	kiss_fft/kiss_fftr.c.o

ifneq ($(SYSTEM_FREEVERB3),true)
OBJS += \
	freeverb/allpass.cpp.o \
	freeverb/biquad.cpp.o \
	freeverb/comb.cpp.o \
	freeverb/delay.cpp.o \
	freeverb/delayline.cpp.o \
	freeverb/earlyref.cpp.o \
	freeverb/efilter.cpp.o \
	freeverb/nrev.cpp.o \
	freeverb/nrevb.cpp.o \
	freeverb/progenitor.cpp.o \
	freeverb/progenitor2.cpp.o \
	freeverb/revbase.cpp.o \
	freeverb/src.cpp.o \
	freeverb/slot.cpp.o \
	freeverb/strev.cpp.o \
	freeverb/utils.cpp.o \
	freeverb/zrev.cpp.o \
	freeverb/zrev2.cpp.o \
	kiss_fft/kiss_fft.c.o \
	kiss_fft/kiss_fftr.c.o
endif

ifneq ($(SYSTEM_LIBSAMPLERATE),true)
OBJS += \
	libsamplerate2/samplerate.c.o \
	libsamplerate2/samplerate_common.c.o \
	libsamplerate2/src_common.c.o \
	libsamplerate2/src_linear.c.o \
	libsamplerate2/src_sinc.c.o \
	libsamplerate2/src_zoh.c.o
endif

all: $(OBJS)

ifneq ($(SYSTEM_LIBSAMPLERATE),true)
libsamplerate2/%.c.o: libsamplerate2/%.c
	$(CC) $< $(BUILD_C_FLAGS) -I. -DLIBSRATE2_FLOAT -c -o $@
endif


ifneq ($(SYSTEM_FREEVERB3),true)
freeverb/%.cpp.o: freeverb/%.cpp
ifneq ($(SYSTEM_LIBSAMPLERATE),true)
	$(CXX) $< $(BUILD_CXX_FLAGS) -I. -DLIBSRATE2_FLOAT -DLIBFV3_FLOAT -Wno-unused-parameter -c -o $@
else
	$(CXX) $< $(BUILD_CXX_FLAGS) -I. -DLIBSRATE1 -DLIBFV3_FLOAT -Wno-unused-parameter -c -o $@
endif
endif

kiss_fft/%.c.o: kiss_fft/%.c
	$(CC) $< $(BUILD_C_FLAGS) -I. -c -o $@

clean:
	rm -f *.[od] */*.[od]
