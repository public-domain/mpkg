include ../config.mk

INCLUDE_FLAGS=-I../include
LIBS=

OBJS=\
	convert.o convertdb.o create.o createdb.o dumpdb.o emit.o install.o \
	md5.o pkg.o pkgdb.o pkgdb_text_file.o pkgdescr.o pkgglobal.o \
	pkgpath.o pkgutil.o rbtree.o remove.o repairdb.o repairdb_pass1.o \
	repairdb_pass2.o repairdb_pass3.o status.o streams.o streams_none.o \
	tar.o unpack.o

ifeq ($(CONFIG_BDB),1)
	OBJS+=pkgdb_bdb.o
endif

ifeq ($(CONFIG_BZIP2),1)
	OBJS+=streams_bzip2.o
endif

ifeq ($(CONFIG_GZIP),1)
	OBJS+=streams_gzip.o
endif

.PHONY: all clean install strip

all: mpkg

$(OBJS): %.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $< $(INCLUDE_FLAGS)

mpkg: $(OBJS)
	$(CC) $(CFLAGS) $(LDFLAGS) -o $@ $(OBJS) $(LIBS)

clean:
	$(RM) -f mpkg $(OBJS)

install: mpkg
	$(INSTALL) -m 0755 -d $(DESTDIR)$(BINDIR)
	$(INSTALL) -m 0755 mpkg $(DESTDIR)$(BINDIR)

strip: mpkg
	$(STRIP) mpkg
