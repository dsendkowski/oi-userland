#
# CDDL HEADER START
#
# The contents of this file are subject to the terms of the
# Common Development and Distribution License (the "License").
# You may not use this file except in compliance with the License.
#
# You can obtain a copy of the license at usr/src/OPENSOLARIS.LICENSE
# or http://www.opensolaris.org/os/licensing.
# See the License for the specific language governing permissions
# and limitations under the License.
#
# When distributing Covered Code, include this CDDL HEADER in each
# file and include the License file at usr/src/OPENSOLARIS.LICENSE.
# If applicable, add the following below this CDDL HEADER, with the
# fields enclosed by brackets "[]" replaced with your own identifying
# information: Portions Copyright [yyyy] [name of copyright owner]
#
# CDDL HEADER END
#

#
# Copyright (c) 2010, 2014, Oracle and/or its affiliates. All rights reserved.
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		ntp
COMPONENT_VERSION=	4.2.8p10
IPS_COMPONENT_VERSION=	$(subst p,.,$(COMPONENT_VERSION))
COMPONENT_SUMMARY=	Network Time Protocol Daemon v4
COMPONENT_DESCRIPTION=	Network Time Protocol v4, NTP Daemon and Utilities
COMPONENT_PROJECT_URL=	http://www.ntp.org/
COMPONENT_SRC=		$(COMPONENT_SRC_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	 \
	sha256:ddd2366e64219b9efa0f7438e06800d0db394ac5c88e13c17b70d0dcdf99b99f
COMPONENT_ARCHIVE_URL=	http://archive.ntp.org/ntp4/ntp-4.2/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI=	service/network/ntp
COMPONENT_CLASSIFICATION=	System/Services
COMPONENT_LICENSE=	ntp license

PATCH_LEVEL = 0

ASLR_MODE= $(ASLR_ENABLE)

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

COMPONENT_BUILD_ARGS=

COMPONENT_PREP_ACTION = ( cd $(@D) && autoreconf --force --install )

CFLAGS +=	-std=c99 -D_XOPEN_SOURCE=600 -D__EXTENSIONS__

CONFIGURE_BINDIR.64 = $(USRSBINDIR)
CONFIGURE_SBINDIR.64 = $(USRSBINDIR)

CONFIGURE_OPTIONS +=	--with-binsubdir=sbin
CONFIGURE_OPTIONS +=	--libexecdir=/usr/lib/inet
CONFIGURE_OPTIONS +=	--sysconfdir=/etc/inet
CONFIGURE_OPTIONS +=	--enable-getifaddrs
CONFIGURE_OPTIONS +=	--enable-all-clocks
CONFIGURE_OPTIONS +=	--enable-debugging
CONFIGURE_OPTIONS +=	--enable-debug-timing
CONFIGURE_OPTIONS +=	--disable-optional-args
CONFIGURE_OPTIONS +=	--enable-parse-clocks
CONFIGURE_OPTIONS +=	--enable-ignore-dns-errors
CONFIGURE_OPTIONS +=	--without-ntpsnmpd
CONFIGURE_OPTIONS +=	--with-openssl-libdir=$(LIBDIR)/$(MACH64)
CONFIGURE_OPTIONS +=	--disable-problem-tests

BUILD_PKG_DEPENDENCIES =	$(BUILD_TOOLS)

COMPONENT_INSTALL_ENV += PATH=/usr/gnu/bin:/usr/bin

# of the build and test and deleting the extra lines, it is easier to just
# cat together all of the logs. The test TEST_PROGNAME3 tests the system
# log facility, so we have to get rid of the output because the pid is
# different every time.
#
# In addition, we append the config.h file so we know if the configuration
# ever changes. We get rid of the version number which changes every time
# we upgrade and the system string and endian info which is different between
# intel and SPARC.

COMPONENT_TEST_CREATE_TRANSFORMS = \
	@if [ -e $(COMPONENT_TEST_MASTER) ]; \
	then \
		print "\#!/bin/sh" > $(COMPONENT_TEST_TRANSFORM_CMD); \
		print '$(FIND) $(BUILD_DIR_64) -name test-\*.log | sort |\\' \
		    >> $(COMPONENT_TEST_TRANSFORM_CMD); \
		print ' xargs cat  | grep -v TEST_PROGNAME3 | \\' \
		    >> $(COMPONENT_TEST_TRANSFORM_CMD); \
		print 'sed -e "s/4.2..p[0-9]*//" \\' \
		    >> $(COMPONENT_TEST_TRANSFORM_CMD); \
		print '> $(COMPONENT_TEST_SNAPSHOT)' \
		    >> $(COMPONENT_TEST_TRANSFORM_CMD); \
		print 'cat $(BUILD_DIR_64)/config.h | \\' \
		    >> $(COMPONENT_TEST_TRANSFORM_CMD); \
		print 'grep -v ENDIAN | grep -v STR_SYSTEM | \\' \
		    >> $(COMPONENT_TEST_TRANSFORM_CMD); \
		print 'grep -v VERSION | grep -v PACKAGE_STRING \\' \
		    >> $(COMPONENT_TEST_TRANSFORM_CMD); \
		print '>> $(COMPONENT_TEST_SNAPSHOT)' \
		    >> $(COMPONENT_TEST_TRANSFORM_CMD); \
	else \
		print 'Cannot find $(COMPONENT_TEST_MASTER)'; \
		exit 2; \
	fi


build:		$(BUILD_64)
install:	$(INSTALL_64)
test:		$(TEST_64)

REQUIRED_PACKAGES += library/libedit
REQUIRED_PACKAGES += library/security/openssl
REQUIRED_PACKAGES += runtime/perl-522
REQUIRED_PACKAGES += service/network/dns/mdns
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/math
