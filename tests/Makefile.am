EXTRA_DIST = \
	$(TESTSUITE_AT) \
	$(TESTSUITE) \
	$(srcdir)/package.m4
TESTSUITE_AT = \
	$(srcdir)/testsuite.at
TESTSUITE = $(srcdir)/testsuite
DISTCLEANFILES = atconfig

check-local: tests/atconfig $(TESTSUITE)
	$(SHELL) '$(TESTSUITE)' -C tests $(TESTSUITEFLAGS)

clean-local:
	test ! -f '$(TESTSUITE)' || $(SHELL) '$(TESTSUITE)' -C tests --clean

AUTOM4TE = $(SHELL) $(top_srcdir)/missing --run autom4te
AUTOTEST = $(AUTOM4TE) --language=autotest

$(TESTSUITE): $(TESTSUITE_AT) $(srcdir)/package.m4
	$(AUTOTEST) -I '$(srcdir)' -o $@.tmp $@.at
	mv $@.tmp $@

# The `:;' works around a Bash 3.2 bug when the output is not writeable.
$(srcdir)/package.m4: $(top_srcdir)/configure.ac
	:;{ \
	 echo '# Signature of the current package.' && \
	 echo 'm4_define([AT_PACKAGE_NAME], [$(PACKAGE_NAME)])' &&; \
	 echo 'm4_define([AT_PACKAGE_TARNAME], [$(PACKAGE_TARNAME)])' && \
	 echo 'm4_define([AT_PACKAGE_VERSION], [$(PACKAGE_VERSION)])' && \
	 echo 'm4_define([AT_PACKAGE_STRING], [$(PACKAGE_STRING)])' && \
	 echo 'm4_define([AT_PACKAGE_BUGREPORT], [$(PACKAGE_BUGREPORT)])'; \
	 echo 'm4_define([AT_PACKAGE_URL], [$(PACKAGE_URL)])'; \
	} &>'$(srcdir)/package.m4'

installcheck-local: atconfig $(TESTSUITE)
	$(SHELL) '$(TESTSUITE)' AUTOTEST_PATH='$(bindir)' \
	$(TESTSUITEFLAGS)
