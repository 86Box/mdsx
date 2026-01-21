ifeq "$(OS)" "Windows_NT"
EXT	?= .dll
else
ifeq "$(shell uname -s)" "Darwin"
EXT	?= .dylib
else
EXT	?= .so
endif
endif
DEST	?= mdsx$(EXT)
CC	?= gcc
STRIP	?= strip
ifeq "$(OS)" "Windows_NT"
CFLAGS	+= -Wl,--out-implib,$(DEST).a
endif
ifneq "$(shell $(CC) -dumpmachine | grep -w i.86)" ""
CFLAGS	+= -march=i386 -msse2 -mfpmath=sse
else
ifneq "$(shell $(CC) -dumpmachine | grep -w x86_64)" ""
CFLAGS	+= -march=x86-64 -msse2 -mfpmath=sse
else
ifneq "$(shell $(CC) -dumpmachine | grep -w arm)" ""
CFLAGS	+= -march=armv7+fp
else
ifneq "$(shell $(CC) -dumpmachine | grep -Ew '(arm|aarch)64')" ""
CFLAGS	+= -march=armv8-a
endif
endif
endif
endif
ifeq "$(DEBUG)" "y"
CFLAGS	+= -DDEBUG -O0 -ggdb
else
CFLAGS	+= -O3
endif

OBJS = edc.c             \
       utils.c           \
       decode.c          \
       common/crc.c      \
       common/crypto.c   \
       common/endian.c   \
       common/gfmul.c    \
       common/xts.c      \
       common/pkcs5.c    \
       crypto/aeskey.c   \
       crypto/aestab.c   \
       crypto/aescrypt.c \
       crypto/bf_ecb.c   \
       crypto/bf_enc.c   \
       crypto/bf_skey.c  \
       crypto/des.c      \
       crypto/des_enc.c  \
       crypto/ecb3_enc.c \
       crypto/set_key.c  \
       crypto/serpent.c  \
       crypto/twofish.c  \
       crypto/c_ecb.c    \
       crypto/c_enc.c    \
       crypto/c_skey.c   \
       crypto/rmd160.c   \
       crypto/sha1.c     \
       crypto/sha2.c     \
       crypto/whirlpool.c

build:
	$(CC) -shared $(CFLAGS) $(OBJS) -I. -fPIC -fomit-frame-pointer -mstackrealign -lz -o $(DEST)
ifneq "$(DEBUG)" "y"
	$(STRIP) -x $(DEST)
endif
