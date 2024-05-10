
SUBDIRS = dio bjt

all:
	for dir in $(SUBDIRS); do \
	$(MAKE) -C $$dir; \
	done

clean:
	for dir in $(SUBDIRS); do \
	$(MAKE) -C $$dir clean; \
	done

install:
	for dir in $(SUBDIRS); do \
	$(MAKE) -C $$dir install; \
	done

TESTDIR = ../ngspice17/tests
GNUCAP = gnucap
# TODO: load with wildcard.
# BUG: depends on attach order.
GNUCAP_ARGS = ${SUBDIRS:%=-a ./%}
include ../Make.test
