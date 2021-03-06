AC_PREREQ(2.53)
AC_INIT([Glasscat], [0.4.0], [daniel.borgmann@gmail.com], [glasscat])
# require automake-1.11 for vala support
AM_INIT_AUTOMAKE([1.11 subdir-objects])
AM_SILENT_RULES([yes])
AC_CONFIG_HEADER(config.h)
AC_CONFIG_MACRO_DIR([m4])

AC_PROG_CC

AC_PATH_PROG(GCONFTOOL, gconftool-2)

PKG_CHECK_MODULES(GLASSCAT, [
	glib-2.0 >= 2.12.0
	gtk+-2.0 >= 2.10.0
	gtksourceview-2.0 >= 2.4.0
	gconf-2.0 >= 2.14.0
	unique-1.0 >= 1.0
])
GLASSCAT_LIBS="${GLASSCAT_LIBS}"
AC_SUBST(GLASSCAT_LIBS)
AC_SUBST(GLASSCAT_CFLAGS)

AC_DEFINE(OLDER_GTK_VERSION,,[Building with older Gtk version]) 

DBUS_GLIB_REQUIRED=0.33
if $PKG_CONFIG --atleast-version $DBUS_GLIB_REQUIRED dbus-glib-1; then
   have_dbus=yes
   PKG_CHECK_MODULES(DBUS, dbus-glib-1 >= $DBUS_GLIB_REQUIRED)
   AC_SUBST(DBUS_CFLAGS)
   AC_SUBST(DBUS_LIBS)
   AC_DEFINE(HAVE_DBUS, , [Building with DBus support]) 
   AC_PATH_PROG(DBUS_BINDING_TOOL, dbus-binding-tool)
else
   have_dbus=no
fi

AM_CONDITIONAL([HAVE_DBUS], [test $have_dbus = yes])

AM_GCONF_SOURCE_2

AC_PROG_LIBTOOL
AC_PATH_PROG(GLIB_GENMARSHAL, glib-genmarshal)

# check for vala
AM_PROG_VALAC([$VALA_REQUIRED])
VAPIDIR=`pkg-config --variable=vapidir vala-1.0`
AC_SUBST(VAPIDIR)


AC_CONFIG_FILES([Makefile])

AC_OUTPUT

dnl ==========================================================================
echo "
                  glasscat $VERSION
                  =============================

        prefix:                    ${prefix}
        C compiler:                ${CC}
        Vala compiler:             ${VALAC}
        cflags:                    ${CFLAGS}
        cppflags:                  ${CPPFLAGS}
        dbus enabled:              ${have_dbus}
        gconf-schema dir:          $GCONF_SCHEMA_FILE_DIR
"
