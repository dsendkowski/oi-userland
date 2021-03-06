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
# Copyright (c) 2014 Alexander Pyhalov
#

include ../../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gnome-system-monitor
COMPONENT_VERSION=	2.28.2
COMPONENT_REVISION=	1
COMPONENT_PROJECT_URL=	http://www.gnome.org
COMPONENT_SUMMARY=	GNOME system monitor
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.bz2
COMPONENT_ARCHIVE_HASH=	\
    sha256:b628edfd39e3a6b374ce133f367d3568475eb4e981a367f4f9d62a9784e5ae59
COMPONENT_ARCHIVE_URL=	http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/2.28/$(COMPONENT_ARCHIVE)

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/configure.mk
include $(WS_MAKE_RULES)/ips.mk

PATH=$(PATH.gnu)

COMPONENT_PREP_ACTION =        ( cd $(@D)  && \
					gnome-doc-common &&\
					libtoolize --force &&\
					intltoolize --force --copy &&\
					aclocal -I . &&\
					autoconf &&\
					autoheader &&\
					automake -c -f -a &&\
					$(TOUCH) pixmaps/side.png )

COMPONENT_PRE_CONFIGURE_ACTION =        (cp -rp $(SOURCE_DIR)/* $(@D) && \
                                        cp -r $(COMPONENT_DIR)/files/po-sun $(@D) && \
                                        cd $(@D)/po-sun && $(MAKE) all )

CONFIGURE_OPTIONS+=	--sysconfdir=/etc
CONFIGURE_OPTIONS+=	--disable-scrollkeeper

CONFIGURE_ENV+= PYTHON="$(PYTHON)"
CONFIGURE_ENV+= PERL="$(PERL)"

CXXFLAGS+= -std=c++11
LDFLAGS += -lgmodule-2.0 -lsocket

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(NO_TESTS)

# Auto-generated dependencies
REQUIRED_PACKAGES += gnome/config/gconf
REQUIRED_PACKAGES += image/library/librsvg
REQUIRED_PACKAGES += library/c++/glibmm
REQUIRED_PACKAGES += library/c++/sigcpp
REQUIRED_PACKAGES += library/desktop/c++/gtkmm
REQUIRED_PACKAGES += library/desktop/cairo
REQUIRED_PACKAGES += library/desktop/gdk-pixbuf
REQUIRED_PACKAGES += library/desktop/gtk2
REQUIRED_PACKAGES += library/desktop/libwnck
REQUIRED_PACKAGES += library/glib2
REQUIRED_PACKAGES += library/libgtop
REQUIRED_PACKAGES += library/libxml2
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/g++-6-runtime
REQUIRED_PACKAGES += system/library/gcc-6-runtime
REQUIRED_PACKAGES += system/library/math
