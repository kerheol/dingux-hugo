#ls /
# HUGO port on PSP
#
HUGO_VERSION=1.1.2

TARGET = dingux-hugo
ZERODEV_PATH	= /opt/gcw0-toolchain/usr/mipsel-gcw0-linux-uclibc/sysroot/usr
BINARIES_PATH	= /opt/gcw0-toolchain/usr/bin
SDL_CONFIG		= $(ZERODEV_PATH)/bin/sdl-config

OBJS = gp2x_psp.o \
Hugo.o \
psp_main.o \
psp_sdl.o \
psp_font.o \
psp_kbd.o \
psp_menu.o \
psp_danzeff.o \
psp_menu_set.o \
psp_menu_help.o \
psp_menu_cheat.o \
psp_menu_list.o \
psp_menu_kbd.o \
psp_menu_joy.o \
psp_editor.o \
psp_fmgr.o \
psp_audio.o \
psp_joy.o \
core/psp/osd_psp_cd.o \
core/psp/osd_psp_mix.o \
core/psp/osd_psp_gfx.o \
core/psp/osd_psp_snd.o \
core/psp/osd_psp_machine.o \
core/psp/osd_psp_keyboard.o \
core/cd.o \
core/dis.o \
core/edit_ram.o \
core/followop.o \
core/format.o \
core/gfx.o \
core/h6280.o \
core/hard_pce.o \
core/hugo.o \
core/list_rom.o \
core/lsmp3.o \
core/mix.o \
core/optable.o \
core/pce.o \
core/pcecd.o \
core/sound.o \
core/sprite.o \
core/utils.o \
core/hcd.o  \
core/miniunz.o  \
core/unzip.o  \
core/bios.o core/cheat.o core/debug.o core/iniconfig.o core/bp.o

CC		= $(BINARIES_PATH)/mipsel-linux-gcc
STRIP	= $(BINARIES_PATH)/mipsel-linux-strip

DEFAULT_CFLAGS = $(shell $(SDL_CONFIG) --cflags)

MORE_CFLAGS = -I. -I$(ZERODEV_PATH)/usr/include \
-Icore -Icore/psp \
-DGCW0_MODE -DNO_STDIO_REDIRECT -DMPU_JZ4740 -DHUGO_VERSION=\"$(HUGO_VERSION)\" \
-mips32 -O3 -D_GNU_SOURCE=1 -D_REENTRANT -DIS_LITTLE_ENDIAN \
-fsigned-char -ffast-math -fomit-frame-pointer \
-fexpensive-optimizations -fno-strength-reduce \
-DUNIX -DBPP16 -DLSB_FIRST -DSOUND  -DNO_STDIO_REDIRECT -O2 \
-DFINAL_RELEASE
# -funroll-loops  -finline-functions

# -DHUGO_OPTIM_IDLE

# -ffast-math -fomit-frame-pointer -fno-strength-reduce
#  -funroll-loops  -finline-functions

# -funroll-loops -ffast-math -fomit-frame-pointer -fno-strength-reduce -finline-functions \
# -pipe -D_GNU_SOURCE=1 -D_REENTRANT -DIS_LITTLE_ENDIAN \


CFLAGS = $(DEFAULT_CFLAGS) $(MORE_CFLAGS)
LDFLAGS = -s
#-static

LIBS += -L$(ZERODEV_PATH)/lib \
-lSDL \
-lSDL_image \
-lpng -lz -lm -lpthread -ldl

.c.o:
	$(CC) $(CFLAGS) -c $< -o $@

$(TARGET): $(OBJS)
	$(CC) $(LDFLAGS) $(CFLAGS) $(OBJS) $(LIBS) -o $(TARGET) && $(STRIP) $(TARGET)

install: $(TARGET)
	cp $< /media/dingux/local/emulators/dingux-hugo/

clean:
	rm -f $(OBJS) $(TARGET)

ctags:
	ctags *[ch]

