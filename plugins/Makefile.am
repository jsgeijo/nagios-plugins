## Process this file with automake to produce Makefile.in

if RELEASE_PRESENT
NP_VERSION = @NP_RELEASE@
else
NP-VERSION-FILE: .FORCE-NP-VERSION-FILE
	@$(SHELL_PATH) $(top_srcdir)/NP-VERSION-GEN
.FORCE-NP-VERSION-FILE:
-include NP-VERSION-FILE
endif

AM_CFLAGS = -DNP_VERSION='"$(NP_VERSION)"'

VPATH = $(top_srcdir) $(top_srcdir)/lib $(top_srcdir)/plugins $(top_srcdir)/plugins/t 

INCLUDES = -I.. -I$(top_srcdir)/lib -I$(top_srcdir)/gl -I$(top_srcdir)/intl @LDAPINCLUDE@ @PGINCLUDE@ @SSLINCLUDE@

localedir = $(datadir)/locale
# gettext docs say to use AM_CPPFLAGS, but per module_CPPFLAGS override this
DEFS = -DLOCALEDIR=\"$(localedir)\" @DEFS@
# gettext docs say to use LDADD, but per module_LDADD override
LIBS = @LTLIBINTL@ @LIBS@
MATHLIBS = @MATHLIBS@

# This is not portable. Run ". tools/devmode" to get development compile flags
#AM_CFLAGS = -Wall

libexec_PROGRAMS = check_apt check_cluster check_disk check_dummy check_http check_load \
	check_mrtg check_mrtgtraf check_ntp check_ntp_peer check_nwstat check_overcr check_ping \
	check_real check_smtp check_ssh check_tcp check_time check_ntp_time \
	check_ups check_users negate \
	urlize @EXTRAS@

check_tcp_programs = check_ftp check_imap check_nntp check_pop \
	check_udp check_clamd @check_tcp_ssl@

EXTRA_PROGRAMS = check_mysql check_radius check_pgsql check_snmp check_hpjd \
	check_swap check_fping check_ldap check_game check_dig \
	check_nagios check_by_ssh check_dns check_nt check_ide_smart	\
	check_procs check_mysql_query check_apt check_dbi

EXTRA_DIST = t tests utils.c netutils.c sslutils.c popen.c utils.h netutils.h \
	popen.h common.h runcmd.c runcmd.h

PLUGINHDRS = common.h

BASEOBJS = utils.o ../lib/libnagiosplug.a ../gl/libgnu.a
NETOBJS = netutils.o $(BASEOBJS) $(EXTRA_NETOBJS)
SSLOBJS = sslutils.o
NETLIBS = $(NETOBJS) $(SOCKETLIBS)

TESTS_ENVIRONMENT = perl -I $(top_builddir) -I $(top_srcdir)

TESTS = @PLUGIN_TEST@

test:
	perl -I $(top_builddir) -I $(top_srcdir) ../test.pl

test-debug:
	NPTEST_DEBUG=1 HARNESS_VERBOSE=1 perl -I $(top_builddir) -I $(top_srcdir) ../test.pl

##############################################################################
# the actual targets

check_apt_LDADD = $(BASEOBJS) runcmd.o
check_cluster_LDADD = $(BASEOBJS)
check_dbi_LDADD = $(NETLIBS) $(DBILIBS)
check_dig_LDADD = $(NETLIBS) runcmd.o 
check_disk_LDADD = $(BASEOBJS) popen.o
check_dns_LDADD = $(NETLIBS) runcmd.o
check_dummy_LDADD = $(BASEOBJS)
check_fping_LDADD = $(NETLIBS) popen.o
check_game_LDADD = $(BASEOBJS) runcmd.o
check_http_LDADD = $(SSLOBJS) $(NETLIBS) $(SSLLIBS)
check_hpjd_LDADD = $(NETLIBS) popen.o
check_ldap_LDADD = $(NETLIBS) $(LDAPLIBS)
check_load_LDADD = $(BASEOBJS) popen.o
check_mrtg_LDADD = $(BASEOBJS)
check_mrtgtraf_LDADD = $(BASEOBJS)
check_mysql_CFLAGS = $(MYSQLCFLAGS) -DNP_VERSION='"$(NP_VERSION)"'
check_mysql_CPPFLAGS = $(MYSQLINCLUDE)
check_mysql_LDADD = $(NETLIBS) $(MYSQLLIBS)
check_mysql_query_CFLAGS = $(MYSQLCFLAGS) -DNP_VERSION='"$(NP_VERSION)"'
check_mysql_query_CPPFLAGS = $(MYSQLINCLUDE)
check_mysql_query_LDADD = $(NETLIBS) $(MYSQLLIBS)
check_nagios_LDADD = $(BASEOBJS) runcmd.o
check_nt_LDADD = $(NETLIBS) 
check_ntp_LDADD = $(NETLIBS) $(MATHLIBS)
check_ntp_peer_LDADD = $(NETLIBS) $(MATHLIBS)
check_nwstat_LDADD = $(NETLIBS)
check_overcr_LDADD = $(NETLIBS)
check_pgsql_LDADD = $(NETLIBS) $(PGLIBS)
check_ping_LDADD = $(NETLIBS) popen.o
check_procs_LDADD = $(BASEOBJS)
check_radius_LDADD = $(NETLIBS) $(RADIUSLIBS)
check_real_LDADD = $(NETLIBS)
check_snmp_LDADD = $(BASEOBJS)
check_smtp_LDADD = $(SSLOBJS) $(NETLIBS) $(SSLLIBS)
check_ssh_LDADD = $(NETLIBS)
check_swap_LDADD = $(MATHLIBS) $(BASEOBJS) popen.o
check_tcp_LDADD = $(SSLOBJS) $(NETLIBS) $(SSLLIBS)
check_time_LDADD = $(NETLIBS)
check_ntp_time_LDADD = $(NETLIBS) $(MATHLIBS)
check_ups_LDADD = $(NETLIBS)
check_users_LDADD = $(BASEOBJS)
check_by_ssh_LDADD = $(NETLIBS)
check_ide_smart_LDADD = $(BASEOBJS)
negate_LDADD = $(BASEOBJS)
urlize_LDADD = $(BASEOBJS) popen.o

check_apt_DEPENDENCIES = check_apt.c $(BASEOBJS) runcmd.o $(DEPLIBS)
check_cluster_DEPENDENCIES = check_cluster.c $(BASEOBJS) $(DEPLIBS)
check_dbi_DEPENDENCIES = check_dbi.c $(NETOBJS) $(DEPLIBS)
check_dig_DEPENDENCIES = check_dig.c $(NETOBJS) runcmd.o $(DEPLIBS)
check_disk_DEPENDENCIES = check_disk.c $(BASEOBJS) popen.o $(DEPLIBS) 
check_dns_DEPENDENCIES = check_dns.c $(NETOBJS) runcmd.o $(DEPLIBS)
check_dummy_DEPENDENCIES = check_dummy.c $(DEPLIBS)
check_fping_DEPENDENCIES = check_fping.c $(NETOBJS) popen.o $(DEPLIBS)
check_game_DEPENDENCIES = check_game.c  $(DEPLIBS) runcmd.o
check_http_DEPENDENCIES = check_http.c $(SSLOBJS) $(NETOBJS) $(DEPLIBS)
check_hpjd_DEPENDENCIES = check_hpjd.c $(NETOBJS) popen.o $(DEPLIBS)
check_ide_smart_DEPENDENCIES = check_ide_smart.c $(BASEOBJS) $(DEPLIBS)
check_ldap_DEPENDENCIES = check_ldap.c $(NETOBJS) $(DEPLIBS)
check_load_DEPENDENCIES = check_load.c $(BASEOBJS) popen.o $(DEPLIBS)
check_mrtg_DEPENDENCIES = check_mrtg.c $(DEPLIBS)
check_mrtgtraf_DEPENDENCIES = check_mrtgtraf.c $(DEPLIBS)
check_mysql_DEPENDENCIES = check_mysql.c $(NETOBJS) $(DEPLIBS)
check_mysql_query_DEPENDENCIES = check_mysql_query.c $(NETOBJS) $(DEPLIBS)
check_nagios_DEPENDENCIES = check_nagios.c $(BASEOBJS) runcmd.o $(DEPLIBS)
check_nt_DEPENDENCIES = check_nt.c $(NETOBJS) $(DEPLIBS)
check_ntp_DEPENDENCIES = check_ntp.c $(NETOBJS) $(DEPLIBS)
check_ntp_peer_DEPENDENCIES = check_ntp_peer.c $(NETOBJS) $(DEPLIBS)
check_nwstat_DEPENDENCIES = check_nwstat.c $(NETOBJS) $(DEPLIBS)
check_overcr_DEPENDENCIES = check_overcr.c $(NETOBJS) $(DEPLIBS)
check_pgsql_DEPENDENCIES = check_pgsql.c $(NETOBJS)  $(DEPLIBS)
check_ping_DEPENDENCIES = check_ping.c $(NETOBJS) popen.o $(DEPLIBS)
check_procs_DEPENDENCIES = check_procs.c $(BASEOBJS) popen.o $(DEPLIBS)
check_radius_DEPENDENCIES = check_radius.c $(NETOBJS)  $(DEPLIBS)
check_real_DEPENDENCIES = check_real.c $(NETOBJS) $(DEPLIBS)
check_snmp_DEPENDENCIES = check_snmp.c $(BASEOBJS) $(DEPLIBS)
check_smtp_DEPENDENCIES = check_smtp.c $(SSLOBJS) $(NETOBJS) $(DEPLIBS)
check_ssh_DEPENDENCIES = check_ssh.c $(NETOBJS) $(DEPLIBS)
check_swap_DEPENDENCIES = check_swap.c $(BASEOBJS) popen.o $(DEPLIBS)
check_tcp_DEPENDENCIES = check_tcp.c $(SSLOBJS) $(NETOBJS) $(DEPLIBS)
check_time_DEPENDENCIES = check_time.c $(NETOBJS) $(DEPLIBS)
check_ntp_time_DEPENDENCIES = check_ntp_time.c $(NETOBJS) $(DEPLIBS)
check_ups_DEPENDENCIES = check_ups.c $(NETOBJS) $(DEPLIBS)
check_users_DEPENDENCIES = check_users.c $(BASEOBJS) popen.o $(DEPLIBS)
check_by_ssh_DEPENDENCIES = check_by_ssh.c $(NETOBJS) $(DEPLIBS)
negate_DEPENDENCIES = negate.c $(BASEOBJS) $(DEPLIBS)
urlize_DEPENDENCIES = urlize.c $(BASEOBJS) popen.o $(DEPLIBS)

##############################################################################
# secondary dependencies

popen.o: popen.c popen.h $(PLUGINHDRS)

runcmd.o: runcmd.c runcmd.h $(PLUGINHDRS)

utils.o: utils.c utils.h $(PLUGINHDRS)

netutils.o: netutils.c netutils.h $(PLUGINHDRS)
sslutils.o: sslutils.c netutils.h $(PLUGINHDRS)

all-local: $(check_tcp_programs)

$(check_tcp_programs): check_tcp
	rm -f $@
	ln -s check_tcp $@

install-exec-hook:
	cd $(DESTDIR)$(libexecdir) && \
	for i in $(check_tcp_programs) ; do rm -f $$i; ln -s check_tcp $$i ; done ;\
	if [ -x check_ldap ] ; then rm -f check_ldaps ; ln -s check_ldap check_ldaps ; fi
	
clean-local:
	rm -f $(check_tcp_programs)
	rm -f NP-VERSION-FILE

uninstall-local:
	cd $(DESTDIR)$(libexecdir) && rm -f $(check_tcp_programs)

