# Created by: Johann Visagie <johann@egenetics.com>
# $FreeBSD$

PORTNAME=	asv
PORTVERSION=	0.5
CATEGORIES=	textproc python
MASTER_SITES=	http://tratt.net/laurie/src/python/asv/releases/
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Extensible Python module to parse simple text file formats like CSV

USE_PYTHON=	yes

PORTDOCS=	INSTALL README THANKS
PORTEXAMPLES=	asv_example.py example_data.csv
PLIST_FILES=	bin/asv \
		%%PYTHON_SITELIBDIR%%/ASV.py \
		%%PYTHON_SITELIBDIR%%/ASV.pyc \
		%%PYTHON_SITELIBDIR%%/ASV.pyo

do-build:
	@${PYTHON_CMD} ${PYTHON_LIBDIR}/compileall.py \
		-d ${PYTHONPREFIX_SITELIBDIR} \
		-f ${WRKSRC}
	@${PYTHON_CMD} -O ${PYTHON_LIBDIR}/compileall.py \
		-d ${PYTHONPREFIX_SITELIBDIR} \
		-f ${WRKSRC}

do-install:
	@printf '#!/bin/sh\n${PYTHON_CMD} ${PYTHONPREFIX_SITELIBDIR}/ASV.py "$$@"\n' \
		> ${WRKDIR}/asv.sh
	${INSTALL_SCRIPT} ${WRKDIR}/asv.sh ${STAGEDIR}${PREFIX}/bin/asv
	@${MKDIR} ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}
	${INSTALL_DATA} ${WRKSRC}/ASV.* ${STAGEDIR}${PYTHONPREFIX_SITELIBDIR}
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${PORTDOCS:S,^,${WRKSRC}/,} ${STAGEDIR}${DOCSDIR}
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	${INSTALL_DATA} ${PORTEXAMPLES:S,^,${WRKSRC}/,} ${STAGEDIR}${EXAMPLESDIR}

.include <bsd.port.mk>
