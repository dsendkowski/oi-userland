#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright (c) 2015 Alexander Pyhalov
#

include ../../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gnome-utils
COMPONENT_VERSION=	2.24.1
# Version was bumped in JDS
IPS_COMPONENT_VERSION=	2.30.0
COMPONENT_REVISION=     1
COMPONENT_PROJECT_URL=	http://www.gnome.org
COMPONENT_SUMMARY=	GNOME log viewer
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH=	\
    sha256:6b7e29feaa25d5e85fa55a00775e7b3296725ef98b455b8b1d810cf379cfdd00
COMPONENT_ARCHIVE_URL=	http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/2.24/$(COMPONENT_ARCHIVE)
COMPONENT_FMRI=		gnome/gnome-log-viewer
COMPONENT_CLASSIFICATION=	Applications/System Utilities
COMPONENT_LICENSE= GPLv3
COMPONENT_LICENSE_FILE= COPYING

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH=$(PATH.gnu)

COMPONENT_PREP_ACTION =        ( cd $(@D)  && \
					libtoolize --copy --force &&\
					glib-gettextize -f &&\
					intltoolize --force --copy &&\
					aclocal -I m4 &&\
					automake -c -f -a &&\
					autoconf )

CFLAGS += -std=c99 $(CPP_XPG6MODE)

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--libexecdir=/usr/lib
CONFIGURE_OPTIONS+=	--disable-scrollkeeper
CONFIGURE_OPTIONS+=	--disable-static
CONFIGURE_OPTIONS+=	--with-grep="/usr/xpg4/bin/grep"

CONFIGURE_ENV+= PYTHON="$(PYTHON)"

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(NO_TESTS)

# Auto-generated dependencies
REQUIRED_PACKAGES += gnome/config/gconf
REQUIRED_PACKAGES += library/desktop/gtk2
REQUIRED_PACKAGES += library/desktop/libgnome
REQUIRED_PACKAGES += library/desktop/libgnomeui
REQUIRED_PACKAGES += library/desktop/pango
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/gnome/gnome-vfs
REQUIRED_PACKAGES += system/library
