###########################################
# Simple Makefile for HIDAPI test program
#
# Alan Ott
# Signal 11 Software
# 2010-06-01
###########################################

all: hidtest

CC=gcc
CXX=g++
COBJS=hid-libusb.o
CPPOBJS=../hidtest/hidtest.o
OBJS=$(COBJS) $(CPPOBJS)
CFLAGS+= $(EXTRA_CFLAGS) -I../hidapi -Wall -g `pkg-config libusb-1.0 --cflags`
LIBS=`pkg-config libusb-1.0 libudev --libs`
# removed libudev, because it's not needed here


hidtest: $(OBJS)
	g++ -Wall -g $^ $(LIBS) -o hidtest

$(COBJS): %.o: %.c
	$(CC) $(CFLAGS) $< -c -o $@

$(CPPOBJS): %.o: %.cpp
	$(CXX) $(CFLAGS) $< -c -o $@

hidapi.so: CFLAGS += -fPIC
hidapi.so: $(COBJS)
	$(CC) $(CFLAGS) -shared $(COBJS) $(LIBS) -o $@

clean:
	-rm -f $(OBJS) hidtest hidapi.so

.PHONY: clean
