# Created by: ports@c0decafe.net
# $FreeBSD$

PORTNAME=	tnote
PORTVERSION=	0.2.1
PORTREVISION=	1
CATEGORIES=	deskutils
MASTER_SITES=	SF/${PORTNAME}/${PORTNAME}/${DISTNAME}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Small note taking program for the terminal

LICENSE=	GPLv3

USES=		shebangfix
USE_PYTHON=		2
USE_PYDISTUTILS=	yes

SHEBANG_FILES=	tnote
python_OLD_CMD=	${SETENV} python
python_CMD=	${SETENV} python2

PLIST_FILES=	bin/tnote man/man1/tnote.1.gz
PORTDOCS=	*

OPTIONS_DEFINE=	DOCS

post-extract:
	@${REINPLACE_CMD} -e 's|share/man|man|; \
		s|share/doc/tnote|${DOCSDIR_REL}|' \
		${WRKSRC}/setup.py

.include <bsd.port.mk>
