AM_CFLAGS =		-Wall -I$(srcdir) \
			-Wstrict-prototypes -Wmissing-prototypes \
			-Wmissing-declarations \
			-Wshadow -Wpointer-arith \
			-Wsign-compare -Wcast-qual \
			-Wno-pointer-sign

bin_PROGRAMS =		httpd

EXTRA_httpd_SOURCES =	compat/imsg.h compat/queue.h compat/tree.h \
			compat/vis.h compat/blf.h

httpd_SOURCES =		compat.h	\
			config.c	\
			config.h	\
			control.c	\
			http.h		\
			httpd.c		\
			httpd.h		\
			log.c		\
			logger.c	\
			parse.y		\
			patterns.c	\
			patterns.h	\
			proc.c		\
			server.c	\
			server_file.c	\
			server_http.c	\
			server_fcgi.c

LDADD =			$(LIBOBJS)

EXTRA_DIST =		README.md

dist_man5_MANS =	httpd.conf.5
dist_man7_MANS =	patterns.7
dist_man8_MANS =	httpd.8
