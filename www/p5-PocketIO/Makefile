# Created by: Sunpoet Po-Chuan Hsieh <sunpoet@FreeBSD.org>
# $FreeBSD$

PORTNAME=	PocketIO
PORTVERSION=	0.14000
CATEGORIES=	www perl5
MASTER_SITES=	CPAN
MASTER_SITE_SUBDIR=	CPAN:VTI
PKGNAMEPREFIX=	p5-
DISTNAME=	${PORTNAME}-${PORTVERSION:C/000$//}

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Socket.IO Plack application

LICENSE=	ART20

BUILD_DEPENDS=	p5-AnyEvent>=0:${PORTSDIR}/devel/p5-AnyEvent \
		p5-JSON>=0:${PORTSDIR}/converters/p5-JSON \
		p5-Protocol-SocketIO>=0.04:${PORTSDIR}/www/p5-Protocol-SocketIO \
		p5-Protocol-WebSocket>=0.00906:${PORTSDIR}/www/p5-Protocol-WebSocket
RUN_DEPENDS:=	${BUILD_DEPENDS}
TEST_DEPENDS=	p5-Plack>=0:${PORTSDIR}/www/p5-Plack \
		p5-Test-TCP>=0:${PORTSDIR}/devel/p5-Test-TCP \
		p5-Twiggy>=0:${PORTSDIR}/www/p5-Twiggy

USE_PERL5=	configure
USES=		perl5

.include <bsd.port.mk>
