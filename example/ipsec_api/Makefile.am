include $(top_srcdir)/example/Makefile.inc

bin_PROGRAMS = odp_ipsec_api

dist_check_SCRIPTS = \
		   odp_ipsec_api_run_ah_in.sh \
		   odp_ipsec_api_run_ah_out.sh \
		   odp_ipsec_api_run_ah_tun_in.sh \
		   odp_ipsec_api_run_ah_tun_out.sh \
		   odp_ipsec_api_run_esp_in.sh \
		   odp_ipsec_api_run_esp_out.sh \
		   odp_ipsec_api_run_esp_tun_in.sh \
		   odp_ipsec_api_run_esp_tun_out.sh \
		   odp_ipsec_api_run_live.sh \
		   odp_ipsec_api_run_router.sh \
		   odp_ipsec_api_run_simple.sh

odp_ipsec_api_SOURCES = \
		    odp_ipsec.c \
		    odp_ipsec_sa_db.c \
		    odp_ipsec_sa_db.h \
		    odp_ipsec_sp_db.c \
		    odp_ipsec_sp_db.h \
		    odp_ipsec_fwd_db.c \
		    odp_ipsec_fwd_db.h \
		    odp_ipsec_cache.c \
		    odp_ipsec_cache.h \
		    odp_ipsec_misc.h

if WITH_OPENSSL
odp_ipsec_api_SOURCES += \
		    odp_ipsec_stream.c \
		    odp_ipsec_stream.h

AM_CPPFLAGS = $(OPENSSL_CPPFLAGS)
LDADD += $(OPENSSL_LIBS)

else
AM_CPPFLAGS = -DNO_OPENSSL
endif

# If building out-of-tree, make check will not copy the scripts and data to the
# $(builddir) assuming that all commands are run locally. However this prevents
# running tests on a remote target using LOG_COMPILER.
# So copy all script and data files explicitly here.
all-local:
	if [ "x$(srcdir)" != "x$(builddir)" ]; then \
		for f in $(dist_check_SCRIPTS); do \
			if [ -e $(srcdir)/$$f ]; then \
				mkdir -p $(builddir)/$$(dirname $$f); \
				cp -f $(srcdir)/$$f $(builddir)/$$f; \
			fi \
		done \
	fi
clean-local:
	if [ "x$(srcdir)" != "x$(builddir)" ]; then \
		for f in $(dist_check_SCRIPTS); do \
			rm -f $(builddir)/$$f; \
		done \
	fi
