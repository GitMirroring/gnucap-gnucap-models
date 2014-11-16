#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.67])
AC_INIT([gnucap-spice3f5], [0.0.1-rc1], [felix@salfelder.org])
AC_CONFIG_HEADERS([config.h])
AC_CONFIG_MACRO_DIR([m4])
AM_INIT_AUTOMAKE
LT_INIT()
AC_LANG(C++)

# Checks for programs.
AC_PROG_CC
AC_PROG_MAKE_SET
AC_PROG_CXX
AC_PROG_LIBTOOL

AS_IF([ test x$program_suffix = xNONE ],,[_program_suffix=$program_suffix])

AC_ARG_WITH([gnucap],
  [AS_HELP_STRING([--with-gnucap], [gnucap location])],
  [],
  [with_gnucap=no])

AS_IF([ test "x$with_gnucap" != xno],[
	CPPFLAGS_KEEP=$CPPFLAGS
	GNUCAP_INCLUDE=
	if test -f $with_gnucap/include/gnucap/spice-wrapper.cc; then
		AC_MSG_NOTICE(suspecting gnucap install prefix)
		GNUCAP_INCLUDE=$with_gnucap/include/gnucap
		gnucap_libdir=$with_gnucap/lib/gnucap
	elif test -f $with_gnucap/include/spice-wrapper.cc; then
		AC_MSG_NOTICE(suspecting gnucap source directory)
		GNUCAP_INCLUDE=$with_gnucap/include
		gnucap_libdir=$prefix/gnucap/lib
	else
		AC_MSG_WARN(dont know what to do)
	fi

	CPPFLAGS+=" -I$srcdir/bjt -I./Include -I$GNUCAP_INCLUDE"
	#abusing CPPFLAGS
	CPPFLAGS+=" -DTRACE_UNTESTED -DSPICE_3f -DPREDICTOR -DAN_pz -DAN_disto -DAN_noise -DHAS_STDLIB -fPIC"
	AC_CHECK_HEADER([spice-wrapper.cc],[
		GNUCAP_INCLUDE=$with_gnucap/include
		GC_CPPFLAGS+=" -I$GNUCAP_INCLUDE"
	],[
		AC_MSG_ERROR([cannot find gnucap headers])
	])
	CPPFLAGS=$CPPFLAGS_KEEP
],[
	AC_CHECK_PROG(HAVE_GCCONF, gnucap-conf$_program_suffix, true, false)

	if test "x$HAVE_GCCONF" = "xfalse"; then
		AC_MSG_ERROR([cannot find gnucap-conf$_program_suffix, see README, try --with-gnucap])
	fi

	GC_CPPFLAGS+=$(gnucap-conf$_program_suffix --cppflags)
	GNUCAP_INCLUDE=$(gnucap-conf$_program_suffix --includedir)
	gnucap_libdir=$(gnucap-conf$_program_suffix --libdir)
] )
AC_SUBST([GC_CPPFLAGS])
AC_SUBST([GNUCAP_INCLUDE])
AC_SUBST([gnucap_libdir])
AC_SUBST([GNUCAP])
GNUCAP=gnucap$_program_suffix

# Checks for libraries.

# Checks for header files.

CPPFLAGS_=$CPPFLAGS
CPPFLAGS=$GC_CPPFLAGS
AC_CHECK_HEADER([bm.h], [ ],
					 [AC_MSG_ERROR([cannot find gnucap headers])])
CPPFLAGS=$CPPFLAGS_


SPICE_INCLUDE=$ac_pwd/Include
AC_SUBST([SPICE_INCLUDE])

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

AC_CONFIG_FILES([Makefile Make2])
AC_OUTPUT

AC_MSG_RESULT([
** Configuration summary for $PACKAGE $VERSION:

   prefix:        $prefix
   GC_CPPFLAGS:   $GC_CPPFLAGS
   GNUCAP_INCLUDE:$GNUCAP_INCLUDE
   plugindir:     $gnucap_libdir
])
