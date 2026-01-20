CC    := gcc
STRIP := strip
PROG  := mdsx

OBJ = edc.c             \
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
ifeq ($(DEBUG), y)
	@$(CC) -shared -Wl,--out-implib,mdsx.dll.a $(OBJ) -I. -ggdb -DDEBUG -O0 -fomit-frame-pointer -mstackrealign -lz -static -o $(PROG).dll
else
	@$(CC) -shared -Wl,--out-implib,mdsx.dll.a $(OBJ) -I. -msse2 -mfpmath=sse -O3 -fomit-frame-pointer -mstackrealign -lz -static -o $(PROG).dll
	@$(STRIP) $(PROG).dll
endif
