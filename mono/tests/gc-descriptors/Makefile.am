CLASS=$(mcs_topdir)/class/lib/$(DEFAULT_PROFILE)

with_mono_path = MONO_PATH=$(CLASS)
RUNTIME = $(with_mono_path) $(top_builddir)/runtime/mono-wrapper
MCS = $(RUNTIME) $(CSC) -unsafe -nowarn:0162 -nowarn:0168 -nowarn:0219 -debug:portable

check-local: test

test : descriptor-tests.exe

descriptor-tests.exe : descriptor-tests.cs
	$(MCS) -Warn:0 descriptor-tests.cs

descriptor-tests.cs : descriptor-tests-driver.cs descriptor-tests-prefix.cs gen-descriptor-tests.py
	if [ "$(srcdir)" != "$(builddir)" ]; then cp $^ .; fi
	$(srcdir)/gen-descriptor-tests.py >descriptor-tests.cs

EXTRA_DIST = descriptor-tests-driver.cs descriptor-tests-prefix.cs gen-descriptor-tests.py

.DELETE_ON_ERROR:

