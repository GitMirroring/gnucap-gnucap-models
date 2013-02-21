
ALL_SUBDIRS=asrc  \
bjt   \
bsim1 \
bsim2 \
cap   \
cccs  \
ccvs  \
csw   \
dio   \
ind   \
isrc  \
jfet  \
ltra  \
mes   \
mos1  \
mos2  \
mos3  \
mos6  \
res   \
sw    \
tra   \
urc   \
vccs  \
vcvs  \
vsrc

SUBDIRS=bjt

DISTHACKFILES=configure install-sh config.sub config.guess Makefile.in aclocal.m4
dist-hack: @PACKAGE_NAME@-@PACKAGE_VERSION@.tar.gz
@PACKAGE_NAME@-@PACKAGE_VERSION@.tar.gz:
	git archive --format=tar --prefix=@PACKAGE_NAME@-@PACKAGE_VERSION@/ HEAD |\
	    tar -xf -
	find $(ALL_SUBDIRS) -name Makefile -exec dirname {} \; | xargs -i mkdir -p @PACKAGE_NAME@-@PACKAGE_VERSION@/{}
	find $(ALL_SUBDIRS) -name Makefile | xargs -i cp {} @PACKAGE_NAME@-@PACKAGE_VERSION@/{}
	cp $(DISTHACKFILES) @PACKAGE_NAME@-@PACKAGE_VERSION@
	tar -czf @PACKAGE_NAME@-@PACKAGE_VERSION@.tar.gz @PACKAGE_NAME@-@PACKAGE_VERSION@

.PHONY: dist-hack
