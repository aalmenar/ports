# Created by: Kim Scarborough <user@unknown.nu>
# $FreeBSD$

PORTNAME=	micro_httpd
PORTVERSION=	2001.12.14
CATEGORIES=	www
MASTER_SITES=	http://www.acme.com/software/micro_httpd/ \
		http://www.unknown.nu/ports/
DISTNAME=	${PORTNAME}_14dec2001

MAINTAINER=	user@unknown.nu
COMMENT=	Extremely small web server

WRKSRC=		${WRKDIR}/${PORTNAME}
PLIST_FILES=	sbin/micro_httpd man/man8/micro_httpd.8.gz

post-patch:
	@${REINPLACE_CMD} -e "s:/usr/local/sbin:${PREFIX}/sbin:g; \
		s:/usr/local/man/man8:${MAN8PREFIX}/man/man8:g; \
		s:gcc:${CC}:g; s:-O:${CFLAGS}:g" \
		${WRKSRC}/Makefile
	@${REINPLACE_CMD} -e "s/^.TH micro_httpd 1/.TH micro_httpd 8/g" \
		${WRKSRC}/micro_httpd.8

.include <bsd.port.mk>
