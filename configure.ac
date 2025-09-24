dnl Process this file with autoconf to produce a configure script.
AC_INIT
AC_CONFIG_SRCDIR([ssmtp.c])

dnl Checks for programs.
AC_PROG_CC
AC_PROG_INSTALL
AC_PROG_LN_S

dnl Checks for libraries.

dnl Checks for header files.
m4_warn([obsolete],
[The preprocessor macro 'STDC_HEADERS' is obsolete.
  Except in unusual embedded environments, you can safely include all
  C89 headers unconditionally.])dnl
# Autoupdate added the next two lines to ensure that your configure
# script's behavior did not change.  They are probably safe to remove.
AC_CHECK_INCLUDES_DEFAULT
AC_PROG_EGREP

AC_CHECK_HEADERS(limits.h strings.h syslog.h unistd.h)


AC_CACHE_CHECK([for obsolete openlog],ssmtp_cv_obsolete_openlog,
	[ AC_COMPILE_IFELSE([AC_LANG_PROGRAM([[#include <syslog.h>  ]], [[ openlog("xx",1);  ]])],[ssmtp_cv_obsolete_openlog=yes],[ssmtp_cv_obsolete_openlog=no])]
)


dnl Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_STRUCT_TM

dnl Checks for libraries.
AC_SEARCH_LIBS(gethostname, nsl)
AC_SEARCH_LIBS(socket, socket)

dnl Checks for library functions.
m4_warn([obsolete],
[your code may safely assume C89 semantics that RETSIGTYPE is void.
Remove this warning and the 'AC_CACHE_CHECK' when you adjust the code.])dnl
AC_CACHE_CHECK([return type of signal handlers],[ac_cv_type_signal],[AC_COMPILE_IFELSE(
[AC_LANG_PROGRAM([#include <sys/types.h>
#include <signal.h>
],
		 [return *(signal (0, 0)) (0) == 1;])],
		   [ac_cv_type_signal=int],
		   [ac_cv_type_signal=void])])
AC_DEFINE_UNQUOTED([RETSIGTYPE],[$ac_cv_type_signal],[Define as the return type of signal handlers
		    ('int' or 'void').])

AC_FUNC_VPRINTF
AC_CHECK_FUNCS(gethostname socket strdup strstr)

dnl Check for optional features
AC_ARG_ENABLE(logfile, 
[  --enable-logfile        additional logging over and above syslog])
if test x$enableval = xyes ; then
	AC_DEFINE(LOGFILE)
fi
enableval=""

AC_ARG_ENABLE(rewrite-domain,
[  --disable-rewrite-domain
                          support for rewriting the sending domain])
if test x$enableval != xno ; then
	AC_DEFINE(REWRITE_DOMAIN)
fi
enableval=""

AC_ARG_ENABLE(ssl,
[  --enable-ssl           support for secure connection to mail server])
if test x$enableval = xyes ; then
	AC_DEFINE(HAVE_SSL)
	LIBS="$LIBS -lssl -lcrypto"
fi
enableval=""

AC_ARG_ENABLE(inet6,
[  --enable-inet6         support for IPv6 transport])
if test x$enableval = xyes ; then
	AC_DEFINE(INET6)
fi
enableval=""

AC_ARG_ENABLE(md5auth,
[  --enable-md5auth         support for MD5 authentication])
if test x$enableval = xyes ; then
	AC_DEFINE(MD5AUTH)
	SRCS="$SRCS md5auth/md5c.c md5auth/hmac_md5.c"
fi
enableval=""
AC_SUBST(SRCS)

AC_CONFIG_FILES([Makefile])
AC_OUTPUT
