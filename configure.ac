AC_INIT([httpd], [7.0], [httpd@omarpolo.com])
AC_CONFIG_LIBOBJ_DIR([compat])
AC_CANONICAL_HOST
AM_INIT_AUTOMAKE([-Wall foreign subdir-objects])
AC_PROG_CC_C99
AC_USE_SYSTEM_EXTENSIONS
AC_PROG_YACC

PKG_PROG_PKG_CONFIG

AC_ARG_WITH([libimsg],
	AS_HELP_STRING([--with-libimsg],
		[Build with imsg-compat library (default: disabled)]))

AC_ARG_WITH([libbsd],
	AS_HELP_STRING([--with-libbsd],
		[Build with libbsd library (default: disabled)]))

AS_IF([test "x$with_libbsd" = "xyes"], [
	PKG_CHECK_MODULES([libbsd], [libbsd-overlay libbsd-ctor], [
		CFLAGS="$libbsd_CFLAGS $CFLAGS"
		LIBS="$libbsd_LIBS $LIBS"
	])
])

AC_REPLACE_FUNCS([
	asprintf		\
	bcrypt_newhash		\
	crypt_newhash		\
	err			\
	explicit_bzero		\
	freezero		\
	getdtablecount		\
	getdtablesize		\
	recallocarray		\
	setproctitle		\
	strlcat			\
	strlcpy			\
	strtonum		\
])

AS_IF([test "x$ac_cv_func_bcrypt_newhash" != "xyes"], [AC_LIBOBJ([blowfish])])

AC_CHECK_HEADERS([sys/tree.h])

AC_MSG_CHECKING([for sys/queue.h with TAILQ_FOREACH_SAFE])
AC_COMPILE_IFELSE([AC_LANG_PROGRAM([
#include <sys/queue.h>
#include <stddef.h>
], [
	TAILQ_HEAD(tailhead, entry) head;
	struct entry {
		TAILQ_ENTRY(entry) entries;
	} *np, *nt;
	TAILQ_INIT(&head);
	TAILQ_FOREACH_SAFE(np, &head, entries, nt) {
		/* nop */ ;
	}
	return 0;
])], [
	AC_MSG_RESULT(yes)
	AC_DEFINE([HAVE_QUEUE_H], 1, [QUEUE_H])
], AC_MSG_RESULT(no))

AC_CHECK_LIB(tls, tls_init, [], [
	AC_MSG_ERROR([requires libtls])
])

dnl use libevent from base on OpenBSD
case "$host_os" in
	*openbsd*)
		AC_CHECK_LIB([event], [event_init], [],
			[AC_MSG_ERROR([requires libevent])])
		;;
	*)
		PKG_CHECK_MODULES([libevent2], [libevent_core >= 2], [
			AC_DEFINE([HAVE_EVENT2], 1, [1 if using event2])
			CFLAGS="$libevent2_CFLAGS $CFLAGS"
			LIBS="$libevent2_LIBS $LIBS"
		], [AC_MSG_ERROR([requires libevent])])
		;;
esac

AS_IF([test "x$with_libimsg" = "xyes"], [
	PKG_CHECK_MODULES([libimsg], [libimsg], [
		CFLAGS="$libimsg_CFLAGS $CFLAGS"
		LIBS="$libimsg_LIBS $LIBS"
	])
])

AC_SEARCH_LIBS([imsg_init], [util], [
		AC_DEFINE([HAVE_IMSG], 1,
			[Define to 1 if you have imsg functions (-lutil or -limsg).])
	], [
		AC_LIBOBJ(imsg)
		AC_LIBOBJ(imsg-buffer)
	]
)

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([
	Makefile
])

AC_OUTPUT
