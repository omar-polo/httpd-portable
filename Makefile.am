AM_CFLAGS =		-Wall -I$(srcdir) \
			-Wstrict-prototypes -Wmissing-prototypes \
			-Wmissing-declarations \
			-Wshadow -Wpointer-arith \
			-Wsign-compare -Wcast-qual

bin_PROGRAMS =		httpd

EXTRA_httpd_SOURCES =	compat/queue.h compat/imsg.h

httpd_SOURCES =		parse.y		\
			config.c	\
			control.c	\
			httpd.c		\
			log.c		\
			logger.c	\
			patterns.c	\
			proc.c		\
			server.c	\
			server_http.c	\
			server_file.c	\
			server_fcgi.c

LDADD =			$(LIBOBJS)

EXTRA_DIST =		README.md

dist_man5_MANS =	httpd.conf.5
dist_man7_MANS =	patterns.7
dist_man8_MANS =	httpd.8
