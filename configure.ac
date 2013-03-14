#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.67])
AC_INIT([gnucap-spice3f5], [0.0.1-rc0], [felix@salfelder.org])
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

AC_ARG_WITH([gnucap],
  [AS_HELP_STRING([--with-gnucap], [gnucap location])],
  [],
  [with_gnucap=no])

AS_IF([ test "x$with_gnucap" != xno],[ 
	GNUCAP_INCLUDE=$with_gnucap/include/gnucap
	GC_CPPFLAGS=-I$GNUCAP_INCLUDE
	gnucap_libdir=$with_gnucap/lib/gnucap
	AC_MSG_CHECKING([gnucap location correctness])
	# FIXME: provided path could be source root or worse
	AC_MSG_RESULT([dont know])
],[ 
	AC_CHECK_PROG(HAVE_GCCONF, gnucap-conf, true, false)

	if test "x$HAVE_GCCONF" = "xfalse"; then
		AC_MSG_ERROR([cannot find gnucap-conf, see README, try --with-gnucap])
	fi

	GC_CPPFLAGS=$(gnucap-conf --cppflags)
	GNUCAP_INCLUDE=$(gnucap-conf --includedir)
	gnucap_libdir=$(gnucap-conf --libdir)
] )
AC_SUBST([GC_CPPFLAGS])
AC_SUBST([GNUCAP_INCLUDE])
AC_SUBST([gnucap_libdir])

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

   prefix:       $prefix
   GC_CPPFLAGS:  $GC_CPPFLAGS
   plugindir:    $gnucap_libdir
])
