#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2016 Adam Stevko
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		zsh-completions
COMPONENT_VERSION=	0.18.0
COMPONENT_SUMMARY=	Additional completion definitions for Zsh.
COMPONENT_PROJECT_URL=	https://github.com/zsh-users/zsh-completions
COMPONENT_FMRI=		utility/$(COMPONENT_NAME)
COMPONENT_CLASSIFICATION= System/Shells
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_VERSION).tar.gz
COMPONENT_ARCHIVE_URL=	https://github.com/zsh-users/zsh-completions/archive/$(COMPONENT_ARCHIVE)
COMPONENT_ARCHIVE_HASH= sha256:b94eb63d044920a4ea6d5d51ae4f237f21b0c3174f3c58ff464b5284477cdb7a
COMPONENT_LICENSE=	Various
COMPONENT_LICENSE_FILE=	$(COMPONENT_NAME).license

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/ips.mk

CLEAN_PATHS += $(BUILD_DIR)

$(BUILD_32):    $(SOURCE_DIR)/.prep
	$(MKDIR) $(@D)
	$(TOUCH) $@

$(INSTALL_32): $(BUILD_32)
	$(MKDIR) $(PROTO_DIR)
	$(MKDIR) $(PROTOUSRSHAREDIR)/$(COMPONENT_NAME)

	$(CP) -a $(SOURCE_DIR)/src/* $(PROTOUSRSHAREDIR)/$(COMPONENT_NAME)

	$(TOUCH) $@

build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(NO_TESTS)
