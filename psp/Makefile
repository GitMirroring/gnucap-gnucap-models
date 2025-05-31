
MGFLAGS =
MODELGEN_VERILOG = gnucap-mg-vams
GNUCAP_CONF = gnucap-conf
GNUCAP_CPPFLAGS = $(shell $(GNUCAP_CONF) --cppflags) -DADD_VERSION -DPIC
CXXFLAGS = -fno-var-tracking-assignments -O0 -Wall -g

all: psp104_n.so psp104_p.so \
     psp104_nqs_n.so psp104_nqs_p.so

%.cc: %.vams
	${MODELGEN_VERILOG} -I psp104 --expand-paramset --nodump-unreachable --nogen-module ${MGFLAGS} -o $@ --cc $<

%.dump: %.vams
	${MODELGEN_VERILOG} -I psp104 --expand-paramset --nodump-unreachable --nodump-module ${MGFLAGS} -o $@ --dump $<

%.o: %.cc
	${CXX} $(GNUCAP_CPPFLAGS) $(CPPFLAGS) -shared -fPIC ${GNUCAP_CXXFLAGS} ${CXXFLAGS} $< -o $@ -c

%.so: %.o
	${CXX} -shared ${GNUCAP_LDFLAGS} ${LDFLAGS} $< -o $@

TESTDIR = tests
include ../Make.test
