bin_PROGRAMS = gmediarender

gmediarender_SOURCES = \
	main.c \
	git-version.h \
	upnp.c \
	upnp.h \
	upnp_control.c \
	upnp_control.h \
	upnp_connmgr.c \
	upnp_connmgr.h \
	upnp_transport.c \
	upnp_transport.h \
	song-meta-data.c \
	song-meta-data.h \
	variable-container.c \
	variable-container.h \
	upnp_device.c \
	upnp_device.h \
	upnp_renderer.c \
	upnp_renderer.h \
	webserver.c \
	webserver.h \
	output.c \
	output.h \
	logging.c \
	logging.h \
	xmldoc.c \
	xmldoc.h \
	xmlescape.c \
	xmlescape.h

if HAVE_GST
gmediarender_SOURCES += \
	output_gstreamer.c \
	output_gstreamer.h
endif

main.c : git-version.h

git-version.h: .FORCE
	$(AM_V_GEN)(echo "#define GM_COMPILE_VERSION \"$(shell git log -n1 --date=short --format='%cd_%h' 2>/dev/null || echo -n '0.0.7-git')\"" > $@-new; \
	cmp -s $@ $@-new || cp $@-new $@; \
	rm $@-new)

.FORCE:

AM_CPPFLAGS = $(GLIB_CFLAGS) $(GST_CFLAGS) $(LIBUPNP_CFLAGS) -DPKG_DATADIR=\"$(datadir)/gmediarender\"
gmediarender_LDADD = $(GLIB_LIBS) $(GST_LIBS) $(LIBUPNP_LIBS) 
