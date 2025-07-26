
MGFLAGS = -a mgopt/nonoise.so
MODELGEN_VERILOG = gnucap-mg-vams
GNUCAP_CONF = gnucap-conf
GNUCAP_CPPFLAGS = $(shell $(GNUCAP_CONF) --cppflags) -DADD_VERSION -DPIC # (gets c++ preprocessor flags from gnucap coniguration)
CXXFLAGS = -fno-var-tracking-assignments -O0 -Wall -g

	
PLUGINS_SO = bsim4.so

PLUGINS_CC = ${PLUGINS_SO:%.so=%.cc}

all: ${PLUGINS_SO}
cc: ${PLUGINS_CC}

%.cc: %.va
	${MODELGEN_VERILOG} --nodump-unreachable --nogen-module --gen-module ${MGFLAGS} -o $@ --cc $<

bsim4_nmos.cc: MGFLAGS += --nogen-module
bsim4_pmos.cc: MGFLAGS += --nogen-module


%.cc: %.vams
	${MODELGEN_VERILOG} --nodump-unreachable --nogen-module --gen-module ${MGFLAGS} -o $@ --cc $<

%.dump: %.vams
	${MODELGEN_VERILOG} --nodump-unreachable --nodump-module ${MGFLAGS} -o $@ --dump $<

%.o: %.cc
	${CXX} $(GNUCAP_CPPFLAGS) $(CPPFLAGS) -shared -fPIC ${GNUCAP_CXXFLAGS} ${CXXFLAGS} $< -o $@ -c

%.so: %.o
	${CXX} -shared ${GNUCAP_LDFLAGS} ${LDFLAGS} $< -o $@

# TODO.
# TESTDIR = ./tests
# TESTCASES = b4_
# GNUCAP_ARGS = -a ./bsim4.so
# include ../../Make.test

.PHONY: cc all
