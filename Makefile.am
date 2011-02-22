EXTRA_DIST = \
	sipxpbx \
	stdprompts \
	sipxecs-lang-@LANG_ID@.spec

promptsdir = $(datadir)/www/doc/stdprompts_@LANG_ID@
prompts_SOURCE = \
	$(shell find $(srcdir)/stdprompts_@LANG_ID@ -name '*.wav' -type f -printf '%P\n')

confdir = @SIPX_JAVADIR@/sipXcommons
conf_DATA = sipxecs-lang-@LANG_ID@.jar

sipxecs-@LANG_ID@.jar :
	jar -cf $@ -C $(srcdir)/sipxpbx .

install-data-hook :
	$(info installing prompts)
	@echo "$$Installer" | \
	  InstallFileList="$(prompts_SOURCE)" \
	  InstallSourceDir=$(srcdir)/stdprompts_@LANG_ID@ \
	  InstallDestDir=$(DESTDIR)$(promptsdir) \
	  bash

# work around INSTALL limitations
# 1.  create directories before installing file 
# 2.  install path1/file into path2/path1/file, not path2/file
define Installer
	for f in $${InstallFileList}; do
	  ThisInstallDir=`dirname $${InstallDestDir}/$$f`
	  $(INSTALL) -d $${ThisInstallDir}
	  $(INSTALL) -t $${ThisInstallDir} $${InstallSourceDir}/$$f
	done;
endef
export Installer