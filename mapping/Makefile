CC=gcc
CPP=g++
PROG=../bin/mapping
COMMON_SRCS=
COMMON_DIR=../mikes-common
SRCS=$(COMMON_DIR)/modules/passive/mikes_logs.c \
     $(COMMON_DIR)/modules/live/ncurses_control.c \
     $(COMMON_DIR)/modules/live/base_module.c \
     $(COMMON_DIR)/modules/passive/pose.c \
     $(COMMON_DIR)/modules/passive/gridmap.c \
     $(COMMON_DIR)/modules/live/gridmapping.c \
     $(COMMON_DIR)/config/config.c \
     $(COMMON_DIR)/bites/util.c \
     $(COMMON_DIR)/bites/mikes.c \
     $(COMMON_DIR)/bites/pngwriter.c \
     $(COMMON_DIR)/modules/live/gui.c \
     $(COMMON_DIR)/modules/live/tim571.c \
     $(COMMON_DIR)/modules/live/t265.c \
     $(COMMON_DIR)/modules/passive/x_base.c \
     $(COMMON_DIR)/modules/passive/x_tim571.c \
     $(COMMON_DIR)/modules/passive/x_xtion.c \
     $(COMMON_DIR)/modules/passive/x_gridmap.c \
     mapping.c \
     core/config_mikes.c \
     ui.c

XTION_SRCS=$(COMMON_DIR)/modules/live/xtion/xtion.cpp
XTION_OBJS=$(COMMON_DIR)/modules/live/xtion/Arm-Release/xtion.o

OPTIMIZE=-O0
DEBUG_FLAGS=-g
CPPSRCS=
OBJS=${SRCS:.c=.o} ${XTION_OBJS}
CPPOBJS=${CPPSRCS:.cpp=.o}
CFLAGS=${OPTIMIZE} ${DEBUG_FLAGS} -std=c11 -D_DEFAULT_SOURCE -D_XOPEN_SOURCE=600 -I. -I/usr/include/cairo -I/usr/local/rplidar/sdk/sdk/include -I/usr/include/librsvg-2.0/librsvg `pkg-config --cflags gio-2.0` -I/usr/include/libxml2 -I/usr/include/gdk-pixbuf-2.0 -Wall
CPPFLAGS=${OPTIMIZE} ${DEBUG_FLAGS} -D_DEFAULT_SOURCE -D_XOPEN_SOURCE=600 -I. -I/usr/include/cairo -I/usr/local/rplidar/sdk/sdk/include -Wall -Wno-write-strings -I/usr/include/librsvg-2.0/librsvg `pkg-config --cflags gio-2.0` -I/usr/include/gdk-pixbuf-2.0
LDFLAGS=${DEBUG_FLAGS} -pthread -lrt -lcairo -lX11 -lm -lncurses -lrealsense2 -latomic -L/usr/local/rplidar/sdk/output/Linux/Release -lrplidar_sdk -lrsvg-2 -lxml2 -lpng -lstdc++ `pkg-config --libs gio-2.0` -lOpenNI

PREFIX=/usr/local
MIKES_CORE=$(shell pwd)
export MIKES_CORE

all: ${OBJS} ${CPPOBJS}
	${CC} ${OBJS} ${CPPOBJS} -o $(PROG) ${CFLAGS} ${LDFLAGS}

${XTION_OBJS}: ${XTION_SRCS}
	$(MAKE) -C $(COMMON_DIR)/modules/live/xtion

install:

test:

uninstall:

clean:
	echo "cleaning"
	rm -f *.o */*.o ${PROG}
	$(MAKE) -C ../mikes-common clean
