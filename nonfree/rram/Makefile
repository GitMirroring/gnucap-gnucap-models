TARGET = rram_v_1_0_0
TESTDIR = tests
# TESTCASES = rr_
GNUCAP_ARGS = -a ./${TARGET}.so
PLUGINS_SO = rram_v_1_0_0.so

include ./MakeBase
include ../../Make.test

all: clean install check 
install: $(PLUGINS_SO)
	@echo "Compile psp103"
clean: $(PLUGINS_SO)
	rm -f $(PLUGINS_SO) $(PLUGINS_SO:%.so=%.o) $(PLUGINS_SO:%.so=%.cc)
	if [ -d check]; then \
		rm -f check/*.out check/*.diff; \
	fi





