
SUBDIRS = 						\
	cmf						\
	illuminant					\
	profiles					\
	figures						\
	ref						\
	tests						\
	ti1

if HAVE_DAEMON
dbusdir = $(sysconfdir)/dbus-1/system.d
dist_dbus_DATA = org.freedesktop.ColorManager.conf

dbusservicemaindir = $(datadir)/dbus-1/system-services
dbusservicemain_in_files = org.freedesktop.ColorManager.service.in
dbusservicemain_DATA     = $(dbusservicemain_in_files:.service.in=.service)
$(dbusservicemain_DATA): $(dbusservicemain_in_files) Makefile
	@sed -e "s|\@servicedir\@|$(libexecdir)|" $< | \
	sed -e "s|\@daemon_user\@|$(daemon_user)|" > $@

systemdservicemain_in_files = colord.service.in

dist_tmpfiles_DATA = colord.conf

endif

if HAVE_SYSTEMD
systemdservicemaindir = $(systemdsystemunitdir)
systemdservicemain_DATA     = $(systemdservicemain_in_files:.service.in=.service)
$(systemdservicemain_DATA): $(systemdservicemain_in_files) Makefile
	@sed -e "s|\@servicedir\@|$(libexecdir)|" $< | \
	sed -e "s|\@daemon_user\@|$(daemon_user)|" > $@
endif

EXTRA_DIST =						\
	$(dbusservicemain_in_files)			\
	org.freedesktop.ColorManager.conf.in

if HAVE_SYSTEMD
EXTRA_DIST += $(systemdservicemain_in_files)
endif

if HAVE_BASH_COMPLETION
bashcompletiondir = $(BASH_COMPLETIONS_DIR)
dist_bashcompletion_DATA = colormgr
endif

CLEANFILES =						\
	$(dist_profile_DATA)

DISTCLEANFILES =					\
	$(dbusservicemain_DATA)				\
	$(systemdservicemain_DATA)

-include $(top_srcdir)/git.mk
