#
# Copyright (c) 2005, 2006, 2007 Thorsten Kukuk <kukuk@thkukuk.de>
# Copyright (c) 2008 Red Hat, Inc.
#

CLEANFILES = *~
MAINTAINERCLEANFILES = $(MANS) README

EXTRA_DIST = README $(XMLS) pam_sepermit.8 sepermit.conf tst-pam_sepermit

if HAVE_LIBSELINUX
  TESTS = tst-pam_sepermit
  man_MANS = pam_sepermit.8
endif

XMLS = README.xml pam_sepermit.8.xml

securelibdir = $(SECUREDIR)
secureconfdir = $(SCONFIGDIR)
sepermitlockdir = ${localstatedir}/run/sepermit

AM_CFLAGS = -I$(top_srcdir)/libpam/include -I$(top_srcdir)/libpamc/include \
	-I$(top_srcdir)/libpam_misc/include \
	-D SEPERMIT_CONF_FILE=\"$(SCONFIGDIR)/sepermit.conf\" \
	-D SEPERMIT_LOCKDIR=\"$(sepermitlockdir)\"

pam_sepermit_la_LIBADD = -L$(top_builddir)/libpam -lpam @LIBSELINUX@
pam_sepermit_la_LDFLAGS = -no-undefined -avoid-version -module
if HAVE_VERSIONING
  pam_sepermit_la_LDFLAGS += -Wl,--version-script=$(srcdir)/../modules.map
endif

if HAVE_LIBSELINUX
  secureconf_DATA = sepermit.conf
  sepermitlock_DATA =

  securelib_LTLIBRARIES = pam_sepermit.la
endif
if ENABLE_REGENERATE_MAN
noinst_DATA = README pam_sepermit.8
README: pam_sepermit.8.xml
-include $(top_srcdir)/Make.xml.rules
endif