
TARGET = jfet
$(TARGET):

include makedefs

HDRS = jfetdefs.h  jfetext.h  jfetitf.h wrapper.h

SPICE_VERSION = SPICE_3f

TESTS = test1 \
        test1e \
        test1t \
        test2a \
        test2b \
        test2 \
        test3 \
        test4a \
        test4 \
        test5a \
        test5

# filter out numerical noise
test1.gc.out: TESTFILTER+=| sed -e 's/181\.6E-21/182\.E-21 /'
test1.gc.out: TESTFILTER+=| sed -e 's/-828.4E-18/ 1.f       /'
test1.gc.out: TESTFILTER+=| sed -e 's/ -4.6332f  / 378.E-18 /'
test1t.gc.out: TESTFILTER+=| sed -e 's/181\.6E-21/182\.E-21 /'
test1t.gc.out: TESTFILTER+=| sed -e 's/-828.4E-18/ 1.f       /'
test1t.gc.out: TESTFILTER+=| sed -e 's/ -4.6332f  / 378.E-18 /'
test2.gc.out: TESTFILTER+=| sed -e 's/577\.4E-18/577\.3E-18/'
test3.gc.out: TESTFILTER+=| sed -e 's/577\.4E-18/577\.3E-18/'
test4.gc.out: TESTFILTER+=| sed -e 's/577\.4E-18/577\.3E-18/'


include ../Make2
