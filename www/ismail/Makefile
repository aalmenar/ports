# Created by: Kelley Reynolds <kelley@insidesystems.net>
# $FreeBSD$

PORTNAME=	ismail
PORTVERSION=	2.1
PORTREVISION=	2
CATEGORIES=	www mail
MASTER_SITES=	http://az.semmy.ru/ISMail/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	PHP-based webmail client

WRKSRC=		${WRKDIR}

NO_BUILD=	yes
USES=		tar:bzip2
USE_PHP=	imap
WANT_PHP_WEB=	yes

PLIST_SUB=	WWWOWN="${WWWOWN}" WWWGRP="${WWWGRP}"
SUB_FILES=	pkg-message

OPTIONS_DEFINE=	DOCS
OPTIONS_SINGLE=	DATASTORE
OPTIONS_SINGLE_DATASTORE=	MYSQL PGSQL
OPTIONS_DEFAULT=	MYSQL

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MMYSQL}
USE_PHP+=	mysql
PLIST_FILES+=	${EXAMPLESDIR_REL}/mysql4.schema
PLIST_DIRS+=	${EXAMPLESDIR_REL}
.endif

.if ${PORT_OPTIONS:MPGSQL}
USE_PHP+=	pgsql
PLIST_FILES+=	${EXAMPLESDIR_REL}/pgsql.schema
PLIST_DIRS+=	${EXAMPLESDIR_REL}
.endif

LIB_DEPENDS+=	libc-client4.so:${PORTSDIR}/mail/cclient

pre-install:
	@${ECHO_MSG} ""
	@${ECHO_MSG} "Inside Systems Mail will be installed to ${WWWDIR}"
	@${ECHO_MSG} "Define WWWDIR to change it."
	@${ECHO_MSG} ""

do-install:
	@${MKDIR} ${STAGEDIR}${WWWDIR}
	${TAR} --exclude '*~' -C ${WRKSRC}/${PORTNAME} -cf - . | ${TAR} -C ${STAGEDIR}${WWWDIR} -xf -
.if ${PORT_OPTIONS:MDOCS}
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/docs.html ${STAGEDIR}${DOCSDIR}
.endif
.if ${PORT_OPTIONS:MMYSQL}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/examples/mysql4.schema ${STAGEDIR}${EXAMPLESDIR}
.endif
.if ${PORT_OPTIONS:MPGSQL}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${WRKSRC}/examples/pgsql.schema ${STAGEDIR}${EXAMPLESDIR}
.endif

post-install:
	@${CAT} ${PKGMEASSAGE}

.include <bsd.port.mk>
