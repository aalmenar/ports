# $FreeBSD$

PORTNAME=	uTox
DISTVERSION=	0.1.8.git20140925
CATEGORIES=	net-im net-p2p

MAINTAINER=	fidaj@ukr.net
COMMENT=	Lightweight Tox client

LICENSE=	GPLv3
LICENSE_FILE=	${WRKSRC}/LICENSE

BUILD_DEPENDS=	${LOCALBASE}/lib/libtoxcore.a:${PORTSDIR}/net-im/tox \
		${LOCALBASE}/include/linux/videodev2.h:${PORTSDIR}/multimedia/v4l_compat
LIB_DEPENDS=	libdbus-1.so:${PORTSDIR}/devel/dbus \
		libXft.so:${PORTSDIR}/x11-fonts/libXft

USE_GITHUB=	yes
GH_ACCOUNT=	notsecure
GH_PROJECT=	${PORTNAME}
GH_TAGNAME=	${GH_COMMIT}
GH_COMMIT=	3f86bb5

USES=		compiler:c11 desktop-file-utils gmake pkgconfig
INSTALLS_ICONS=	yes

post-install:
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/bin/utox

.include <bsd.port.mk>
