#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2015 Alexander Pyhalov
# Copyright 2016 Aurelien Larcher
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=           freetype
COMPONENT_VERSION=        2.8.1
COMPONENT_FMRI=           system/library/freetype-2
COMPONENT_CLASSIFICATION= System/Libraries
COMPONENT_SUMMARY=  	FreeType 2 font engine
COMPONENT_SRC=      	$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH= \
  sha256:e5435f02e02d2b87bb8e4efdcaa14b1f78c9cf3ab1ed80f94b6382fb6acc7d78
COMPONENT_ARCHIVE_URL= \
  http://download.savannah.gnu.org/releases/freetype/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://freetype.org/
COMPONENT_LICENSE=      The FreeType Project License
COMPONENT_LICENSE_FILE= freetype-2.license

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH=$(PATH.gnu)

gcc_OPT=-O2

CONFIGURE_OPTIONS+= --disable-static
CONFIGURE_OPTIONS+= --enable-shared
CONFIGURE_OPTIONS+= --enable-biarch-config
CONFIGURE_OPTIONS+= --with-zlib
CONFIGURE_OPTIONS+= --with-bzip2
CONFIGURE_OPTIONS+= --with-png
CONFIGURE_OPTIONS+= --with-harfbuzz
CONFIGURE_OPTIONS+= --with-pic

COMPONENT_PREP_ACTION = ( cd $(@D); \
	$(GSED) -ri 's:.*(AUX_MODULES.*valid):\1:' modules.cfg && \
	$(GSED) -r 's:.*(\#.*SUBPIXEL_RENDERING) .*:\1:' \
		-i include/freetype/config/ftoption.h ) 

build: $(BUILD_32_and_64)

install: $(INSTALL_32_and_64)

test: $(TEST_32_and_64)

REQUIRED_PACKAGES += compress/bzip2
REQUIRED_PACKAGES += image/library/libpng16
REQUIRED_PACKAGES += library/c++/harfbuzz
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += system/library
