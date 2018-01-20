#!/usr/bin/make -f
#
# Makefile for the Debian package of listSerialPortsC
#

JAVA_HOME = /usr/lib/jvm/default-java
JAVA_INCLUDE_PATH = $(JAVA_HOME)/include

CC = gcc
RM = rm -f

# Define listSerialsj variables
LSJ_NAME = listSerialsj
LSJ_MAYOR = 1
LSJ_MINOR = 4
LSJ_RELEASE = 0
LSJ_LINKERNAME = lib$(LSJ_NAME).so
LSJ_SONAME = $(LSJ_LINKERNAME).$(LSJ_MAYOR)
LSJ_REALNAME = $(LSJ_SONAME).$(LSJ_MINOR).$(LSJ_RELEASE)
LSJ_SRCS = jnilib.c
LSJ_OBJS = $(LSJ_SRCS:.c=.o)
$(LSJ_REALNAME): CUSTOM_CFLAGS =-fPIC -I$(JAVA_INCLUDE_PATH)\
	-I$(JAVA_INCLUDE_PATH)/linux
$(LSJ_REALNAME): CUSTOM_LDFLAGS = -shared -lserialport

.PHONY: all
all: $(LSJ_REALNAME)

$(LSJ_REALNAME): $(LSJ_OBJS)
	$(CC) $(LDFLAGS) $(CUSTOM_LDFLAGS) -Wl,-soname,$(LSJ_SONAME) -o $@ $^
	ln -sf $@ $(LSJ_SONAME)
	ln -sf $(LSJ_SONAME) $(LSJ_LINKERNAME)

%.o: %.c
	$(CC) $(CFLAGS) $(CPPFLAGS) $(CUSTOM_CFLAGS) -c -o $@ $<

.PHONY: clean
clean:
	-${RM} *.so* *.o
