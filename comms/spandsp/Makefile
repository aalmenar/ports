# Created by: wlloyd@slap.net
# $FreeBSD$

PORTNAME=	spandsp
PORTVERSION=	0.0.5
PORTREVISION=	1
CATEGORIES=	comms
MASTER_SITES=	http://www.soft-switch.org/downloads/spandsp/ \
		http://www.soft-switch.org/downloads/spandsp/old/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	DSP library and software FAX machine

LIB_DEPENDS=	libtiff.so:${PORTSDIR}/graphics/tiff

GNU_CONFIGURE=	yes
INSTALL_TARGET=	install-strip
USES=		autoreconf gmake libtool tar:tgz

CPPFLAGS+=	-I${LOCALBASE}/include
LIBS+=		-L${LOCALBASE}/lib

USE_LDCONFIG=	yes

CONFLICTS=	spandsp-devel-[0-9]*

.include <bsd.port.mk>
