# Makefile.am for the SDL Rich Text Format loading library and viewer

lib_LTLIBRARIES = libSDL2_rtf.la

libSDL2_rtfincludedir = $(includedir)/SDL2
libSDL2_rtfinclude_HEADERS =	\
	SDL_rtf.h

libSDL2_rtf_la_SOURCES =		\
	rtfactn.c		\
	rtfdecl.h		\
	rtfreadr.c		\
	rtftype.h		\
	SDL_rtfreadr.c		\
	SDL_rtfreadr.h		\
	SDL_rtf.c

EXTRA_DIST =			\
	version.rc		\
	SDL_rtf.spec		\
	SDL_rtf.spec.in		\
	gcc-fat.sh		\
	autogen.sh			\
	$(srcdir)/*.txt

if USE_VERSION_RC
libSDL2_rtf_la_LDFLAGS = 	\
	-no-undefined		\
	-release $(LT_RELEASE)	\
	-version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE) -Wl,version.o
libSDL2_rtf_la_DEPENDENCIES = version.o
else
libSDL2_rtf_la_LDFLAGS = 	\
	-no-undefined		\
	-release $(LT_RELEASE)	\
	-version-info $(LT_CURRENT):$(LT_REVISION):$(LT_AGE)
endif

%.o : %.rc
	$(WINDRES) $< $@

if HAVE_SDL_TTF
EXAMPLES = showrtf
else
EXAMPLES =
endif
noinst_PROGRAMS = $(EXAMPLES)

showrtf_SORUCES = showrtf.c
showrtf_LDADD = libSDL2_rtf.la -lSDL2_ttf

# Rule to build tar-gzipped distribution package
$(PACKAGE)-$(VERSION).tar.gz: distcheck

# Rule to build RPM distribution package
rpm: $(PACKAGE)-$(VERSION).tar.gz
	rpmbuild -ta $(PACKAGE)-$(VERSION).tar.gz

