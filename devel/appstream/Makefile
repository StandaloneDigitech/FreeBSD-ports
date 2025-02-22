# Some knobs are defined with ?= and += to allow them
# being overriden by devel/appstream-qt slave port

PORTNAME?=	AppStream
DISTVERSION=	1.0.3
PORTREVISION?=	1
CATEGORIES=	devel
MASTER_SITES=	https://www.freedesktop.org/software/${PORTNAME:tl}/releases/

PATCH_SITES=	https://github.com/ximion/appstream/commit/
PATCHFILES=	da31a9318e53cf0310637773ca26eaa910782a7d.patch:-p1

MAINTAINER=	desktop@FreeBSD.org
COMMENT?=	Machine-readable software metadata for desktop environments
WWW=		https://www.freedesktop.org/wiki/Distributions/AppStream/

LICENSE=	GPLv2+ LGPL21+
LICENSE_COMB=	multi

BUILD_DEPENDS=	docbook-xsl>=0:textproc/docbook-xsl \
		gperf>0:devel/gperf \
		itstool:textproc/itstool \
		lmdb>0:databases/lmdb
LIB_DEPENDS?=	libcurl.so:ftp/curl \
		libstemmer.so:textproc/snowballstemmer \
		libxmlb.so:textproc/libxmlb \
		libyaml.so:textproc/libyaml \
		libzstd.so:archivers/zstd

USES+=		gettext gnome localbase:ldflags meson pkgconfig \
		python:build tar:xz vala:build

USE_GNOME+=	glib20 introspection:build libxml2 libxslt:build
USE_LDCONFIG=	yes

MESON_ARGS+=	-Dstemming=true \
		-Dvapi=true \
		-Dapidocs=false \
		-Dinstall-docs=false \
		-Dsystemd=false

post-patch:
	${REINPLACE_CMD} \
		-e 's|APPLICATIONS_DIR = "/usr/share/applications"|APPLICATIONS_DIR = "${LOCALBASE}/share/applications"|' \
		-e 's|METAINFO_DIR = "/usr/share/metainfo"|METAINFO_DIR = "${LOCALBASE}/share/metainfo"|' \
		-e 's|"/usr/share",|"${LOCALBASE}/share",|' \
		${WRKSRC}/src/as-pool.c
	${REINPLACE_CMD} \
		-e 's|"/usr/share";|"${LOCALBASE}/share";|' \
		${WRKSRC}/src/as-utils.c

.include <bsd.port.mk>
