#
# Copyright (c) 2005, 2006, 2009, 2010 Thorsten Kukuk <kukuk@suse.de>
#

CLEANFILES = *~
MAINTAINERCLEANFILES = $(MANS) README

EXTRA_DIST = $(DATA) $(MANS) $(XMLS) $(TESTS)

if HAVE_DOC
man_MANS = pam_tty_audit.8
endif
XMLS = README.xml pam_tty_audit.8.xml
TESTS = tst-pam_tty_audit

securelibdir = $(SECUREDIR)

AM_CFLAGS = -I$(top_srcdir)/libpam/include -I$(top_srcdir)/libpamc/include \
	$(WARN_CFLAGS)
AM_LDFLAGS = -no-undefined -avoid-version -module
if HAVE_VERSIONING
  AM_LDFLAGS += -Wl,--version-script=$(srcdir)/../modules.map
endif

pam_tty_audit_la_LIBADD = $(top_builddir)/libpam/libpam.la
securelib_LTLIBRARIES = pam_tty_audit.la

if ENABLE_REGENERATE_MAN
noinst_DATA = README
-include $(top_srcdir)/Make.xml.rules
endif
