# Created by: Sunpoet Po-Chuan Hsieh <sunpoet@FreeBSD.org>
# $FreeBSD$

PORTNAME=	Type-Tiny-XS
PORTVERSION=	0.012
CATEGORIES=	devel perl5
MASTER_SITES=	CPAN
MASTER_SITE_SUBDIR=	CPAN:TOBYINK
PKGNAMEPREFIX=	p5-

MAINTAINER=	sunpoet@FreeBSD.org
COMMENT=	Tiny, yet Moo(se)-compatible type constraint

LICENSE=	ART10 GPLv1
LICENSE_COMB=	dual

USE_PERL5=	configure
USES=		perl5

post-install:
	${CHMOD} u+w ${STAGEDIR}${SITE_PERL}/${PERL_ARCH}/auto/Type/Tiny/XS/XS.so
	${STRIP_CMD} ${STAGEDIR}${SITE_PERL}/${PERL_ARCH}/auto/Type/Tiny/XS/XS.so
	${CHMOD} u-w ${STAGEDIR}${SITE_PERL}/${PERL_ARCH}/auto/Type/Tiny/XS/XS.so

.include <bsd.port.mk>
