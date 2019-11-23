AM_CFLAGS = @DBUS_CFLAGS@ @XML_CFLAGS@ @SELINUX_CFLAGS@
if PIE
AM_CFLAGS += -fPIC
endif

man_MANS = oddjob-gpupdate.conf.5 oddjobd-gpupdate.conf.5
man_MANS += pam_oddjob_gpupdate.8

confddir = $(sysconfdir)/oddjobd.conf.d
confd_DATA = oddjobd-gpupdate.conf

CLEANFILES = $(confd_DATA)

systemdbusdir = $(sysconfdir)/@DBUS_PACKAGE@/system.d
systemdbus_DATA = oddjob-gpupdate.conf
pkglibexec_PROGRAMS = gpupdate
pkglibexecdir = $(libexecdir)/oddjob

noinst_SCRIPTS = gpupdatefor gpupdateforme

libsecuritydir = $(libdir)/security
libsecurity_LTLIBRARIES = pam_oddjob_gpupdate.la

lib_LTLIBRARIES =
noinst_LTLIBRARIES =
noinst_DATA =
noinst_HEADERS = oddjob.h

noinst_LTLIBRARIES += liboddcommon.la liboddselinux.la
liboddcommon_la_SOURCES = \
	buffer.c buffer.h \
	util.c \
	util.h \
	common.h
liboddselinux_la_SOURCES = \
	selinux.h \
	selinux.c \
	common.h

gpupdate_SOURCES = \
	common.h \
	handlers.h \
	selinux.h \
	gpupdate.c
gpupdate_LDADD = liboddcommon.la liboddselinux.la @SELINUX_LIBS@
gpupdate_LDFLAGS =
if PIE
gpupdate_LDFLAGS += -fPIE -pie
endif
if NOW
gpupdate_LDFLAGS += -Wl,-z,relro,-z,now
endif

pam_oddjob_gpupdate_la_SOURCES = \
	common.h \
	oddjob_dbus.c \
	oddjob_dbus.h \
	mainloop.c \
	mainloop.h \
	pam_oddjob_gpupdate.c
pam_oddjob_gpupdate_la_LIBADD = liboddcommon.la @DBUS_LIBS@ @PAM_LIBS@ @SELINUX_LIBS@
pam_oddjob_gpupdate_la_LDFLAGS = -module -avoid-version -export-symbols-regex "pam_sm_.*"

if NOW
pam_oddjob_gpupdate_la_LDFLAGS += -Wl,-z,relro,-z,now
endif
