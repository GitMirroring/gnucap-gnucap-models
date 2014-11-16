#! /bin/sh
#
# Run the various GNU autotools to bootstrap the build
# system.  Should only need to be done once.

# for now avoid using bash as not everyone has that installed
CONFIG_SHELL=/bin/sh
export CONFIG_SHELL

libtoolize -c -f -i

echo "Running aclocal..."
aclocal -I m4 $ACLOCAL_FLAGS || exit 1

echo "Running autoheader..."
autoheader || exit 1

echo "Running automake..."
automake -a -c --gnu  || exit 1

echo "Running autoconf..."
autoconf || exit 1

if [ -r config.status ]; then
	CMD="./config.status --recheck"
	echo "Running $CMD $@ ..."
	$CMD
else
	echo now run \"./configure --stuff\"
fi
