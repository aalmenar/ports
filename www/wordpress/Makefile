# Created by: Elvis Chiang <elvis@sslab.cs.ccu.edu.tw>
# $FreeBSD$

PORTNAME=	wordpress
PORTVERSION=	4.1
PORTEPOCH=	1
CATEGORIES=	www
MASTER_SITES=	http://wordpress.org/

MAINTAINER=	ychsiao@ychsiao.org
COMMENT=	State-of-the-art semantic personal publishing platform

LICENSE=	GPLv2

CONFLICTS_INSTALL=	de-wordpress-[0-9].* ja-wordpress-[0-9].* ru-wordpress-[0-9].*

NO_BUILD=	yes
USES=		cpe
USE_PHP=	curl gd hash mysql pcre tokenizer xml zip zlib
WANT_PHP_WEB=	yes
WRKSRC=		${WRKDIR}/${PORTNAME}

.if ${PORTVERSION:N*.*.*}
CPE_VERSION=	${PORTVERSION}.0
.endif

SUB_FILES=	pkg-message
PLIST=		${WRKDIR}/pkg-plist
PORTDOCS=	license.txt readme.html

OPTIONS_DEFINE=	DOCS

pre-everything::
	@${ECHO_CMD} "If you want to upgrade, you must read upgrade document."
	@${ECHO_CMD} ""
	@sleep 1

pre-install:
	${ECHO_CMD} '@owner www' > ${PLIST}
	${ECHO_CMD} '@group www' >> ${PLIST}
	cd ${WRKSRC}/ && ${FIND} -s * -type f | ${SED} -e 's|^|%%WWWDIR%%/|' >> ${PLIST}
	${ECHO_CMD} '@owner' >> ${PLIST}
	${ECHO_CMD} '@group' >> ${PLIST}
	if [ ! -f ${WRKSRC}/wp-config-sample.php ]; then ${CP} \
		${WRKSRC}/wp-config.php.sample ${WRKSRC}/wp-config.php; fi

do-install:
	${INSTALL} -d -m 755 ${STAGEDIR}${WWWDIR}/
	${CP} -R ${WRKSRC}/ ${STAGEDIR}${WWWDIR}/
	${FIND} ${STAGEDIR}${WWWDIR}/ -type d -exec ${CHMOD} g+w '{}' \;
	${MKDIR} ${STAGEDIR}${DOCSDIR}/
	cd ${WRKSRC}/ && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}/

.include <bsd.port.mk>
