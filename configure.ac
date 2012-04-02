# Process this file with autoconf to produce a configure script.
AC_INIT([scim-input-pad],[0.1.3.1],[suzhe@tsinghua.org.cn])
AC_CONFIG_SRCDIR([src/scim_input_pad.cpp])

SCIM_VERSION=1.4.0
# GTK_VERSION=2.4.0

AC_SUBST(SCIM_VERSION)
# AC_SUBST(GTK_VERSION)

# libtool versioning for SCIM Input Pad

# increment if the interface has additions, changes, removals.
SCIM_INPUT_PAD_CURRENT=1

# increment any time the source changes; set to 0 if you increment CURRENT
SCIM_INPUT_PAD_REVISION=0

# increment if any interfaces have been added; set to 0
# if any interfaces have been removed. removal has 
# precedence over adding, so set to 0 if both happened.
SCIM_INPUT_PAD_AGE=1

AC_SUBST(SCIM_INPUT_PAD_CURRENT)
AC_SUBST(SCIM_INPUT_PAD_REVISION)
AC_SUBST(SCIM_INPUT_PAD_AGE)
SCIM_INPUT_PAD_VERSION=$SCIM_INPUT_PAD_CURRENT.$SCIM_INPUT_PAD_REVISION.$SCIM_INPUT_PAD_AGE

GETTEXT_PACKAGE=scim-input-pad
AC_SUBST(GETTEXT_PACKAGE)
AC_DEFINE_UNQUOTED(GETTEXT_PACKAGE,"$GETTEXT_PACKAGE", [The gettext domain])

# Init automake stuff
AM_INIT_AUTOMAKE
AC_CONFIG_HEADERS([config.h])

#AC_REQUIRE(AC_CANONICAL_HOST)_LT_SET_OPTION([LT_INIT],[win32-dll])
#AC_DIAGNOSE([obsolete],[AC_LIBTOOL_WIN32_DLL: Remove this warning and the call to _LT_SET_OPTION when you
#put the `win32-dll' option into LT_INIT's first parameter.])

LT_CONFIG_LTDL_DIR([libltdl])
LT_INIT([dlopen])
LTDL_INIT
AC_SUBST(LIBTOOL_DEPS)

AC_PROG_CXX
AC_PROG_CC
AC_LANG(C++)

AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T

# Init gettext
ALL_LINGUAS="zh_CN zh_TW pa ja de fr it nl"
AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION([0.14.1])

# Check intltool
IT_PROG_INTLTOOL([0.33], [no-xml])

# Check SCIM 
PKG_CHECK_MODULES(SCIM,[scim >= $SCIM_VERSION])

# Check gtk2
# PKG_CHECK_MODULES(GTK2, [gtk+-2.0 >= 2.4.0])
PKG_CHECK_MODULES(GTK2, [gtk+-2.0 >= 2.4.0],
            [SCIM_INPUT_PAD_HAS_GTK2=yes],
            [SCIM_INPUT_PAD_HAS_GTK2=no])

PKG_CHECK_MODULES(GTK3, [gtk+-3.0 >= 3.0.0],
            [SCIM_INPUT_PAD_HAS_GTK3=yes],
            [SCIM_INPUT_PAD_HAS_GTK3=no])


# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([libintl.h dirent.h])

# libtool option to control which symbols are exported
# right now, symbols starting with _ are not exported
LIBTOOL_EXPORT_OPTIONS='-export-symbols-regex "^[[^_]].*"'
AC_SUBST(LIBTOOL_EXPORT_OPTIONS)

# Extra args.
AC_ARG_ENABLE(debug,
	      [  --enable-debug            Turn on debugging],
       	      enable_debug=yes,
	      enable_debug=no)

AC_ARG_WITH(gtk-version,
        AS_HELP_STRING([--with-gtk-version=2 or 3],
        [Select gtk version if both gtk2 and gtk3 are available (default is 3)]),
		[WANT_GTK_VERSION=$withval],
        [WANT_GTK_VERSION=3])

if test "$SCIM_INPUT_PAD_HAS_GTK3" = "yes" \
	-a "$SCIM_INPUT_PAD_HAS_GTK2" = "yes"; then
  if test "$WANT_GTK_VERSION" = "2"; then
    USE_GTK_VERSION=2
  else
    USE_GTK_VERSION=3
  fi
elif test "$SCIM_INPUT_PAD_HAS_GTK3" = "yes"; then
  USE_GTK_VERSION=3
elif test "$SCIM_INPUT_PAD_HAS_GTK2" = "yes"; then
  USE_GTK_VERSION=2 
else
  AC_MSG_ERROR([GTK >= 2.4 can not be found!])
fi

if test "$USE_GTK_VERSION" = "3"; then
  GTK_VERSION=3.0.0
  GTK_MAJOR_VERSION=3
  GTK_BINARY_VERSION=`$PKG_CONFIG --variable=gtk_binary_version gtk+-3.0`
  GTK_LIBDIR=`$PKG_CONFIG --variable=libdir gtk+-3.0`
  GTK_CFLAGS=$GTK3_CFLAGS
  GTK_LIBS=$GTK3_LIBS
else
  GTK_VERSION=2.4.0
  GTK_MAJOR_VERSION=2
  GTK_BINARY_VERSION=`$PKG_CONFIG --variable=gtk_binary_version gtk+-2.0`
  GTK_LIBDIR=`$PKG_CONFIG --variable=libdir gtk+-2.0`
  GTK_CFLAGS=$GTK2_CFLAGS
  GTK_LIBS=$GTK2_LIBS
fi

AC_SUBST(GTK_VERSION)
AC_SUBST(GTK_MAJOR_VERSION)
AC_SUBST(GTK_BINARY_VERSION)
AC_SUBST(GTK_LIBDIR)
AC_SUBST(GTK_CFLAGS)
AC_SUBST(GTK_LIBS)

if test "$enable_debug" = "yes"; then
  AC_DEFINE(ENABLE_DEBUG,1,[Define this to enable the debug facility in libscim])
  CFLAGS="$CFLAGS -g"
  CXXFLAGS="$CXXFLAGS -g"
fi

SCIM_ICONDIR=`$PKG_CONFIG --variable=icondir scim`
SCIM_MODULEDIR=`$PKG_CONFIG --variable=moduledir scim`
SCIM_DATADIR=`$PKG_CONFIG --variable=scimdatadir scim`
SCIM_LIBEXECDIR=`$PKG_CONFIG --variable=moduledir scim`

if test "x$SCIM_ICONDIR" = "x"; then
  SCIM_ICONDIR=${datadir}/scim/icons
fi

if test "x$SCIM_MODULEDIR" = "x"; then
  SCIM_MODULEDIR=${libdir}/scim-1.0
fi

if test "x$SCIM_DATADIR" = "x"; then
  SCIM_DATADIR=${datadir}/scim
fi

if test "x$SCIM_LIBEXECDIR" = "x"; then
  SCIM_LIBEXECDIR=${libdir}/scim-1.0
fi

AC_SUBST(SCIM_ICONDIR)
AC_SUBST(SCIM_MODULEDIR)
AC_SUBST(SCIM_DATADIR)
AC_SUBST(SCIM_LIBEXECDIR)

SCIM_INPUT_PAD_DATADIR=$SCIM_DATADIR/input-pad
SCIM_INPUT_PAD_USER_DATADIR=/.scim/input-pad

AC_SUBST(SCIM_INPUT_PAD_DATADIR)
AC_SUBST(SCIM_INPUT_PAD_USER_DATADIR)

AC_CONFIG_FILES([Makefile po/Makefile.in
		data/Makefile
		data/scim-input-pad
		data/base.pad
		data/keyboard.pad
		data/japanese.pad
		data/chinese.pad
		data/korean.pad
		data/arabian.pad
		data/ethiopic.pad
		data/india_bengali.pad
		data/india_chiki.pad
		data/india_devanagari.pad
		data/india_gujarati.pad
		data/india_gurmukhi.pad
		data/india_kannada.pad
		data/india_lepcha.pad
		data/india_limbu.pad
		data/india_malayalam.pad
		data/india_oriya.pad
		data/india_saurashtra.pad
		data/india_sinhala.pad
		data/india_syloti_nagri.pad
		data/india_tamil.pad
		data/india_telugu.pad
		data/armenian.pad
		data/balinese.pad
		data/buginese.pad
		data/cham.pad
		data/georgian.pad
		data/hebrew.pad
		data/kaya.pad
		data/khmer.pad
		data/lao.pad
		data/myanmar.pad
		data/mongolian.pad
		data/philipine_buhid.pad
		data/philipine_hanunoo.pad
		data/philipine_tagalog.pad
		data/russian.pad
		data/tai_lue.pad
		data/rejang.pad
		data/sundanese.pad
		data/tai_le.pad
		data/thai.pad
		data/tibet.pad
		src/Makefile
		scim-input-pad.spec])
AC_OUTPUT

AC_MSG_RESULT([
Build options:
  Version                  $SCIM_INPUT_PAD_VERSION
  Install prefix           $prefix
  Build shared libs        $enable_shared
  Build static libs        $enable_static
  Enable debug             $enable_debug

Module options:           
  GTK Version              $USE_GTK_VERSION
])

