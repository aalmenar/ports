# $FreeBSD$

PORTNAME=	senna
PORTVERSION=	1.1.5
PORTREVISION=	1
PORTEPOCH=	1
CATEGORIES=	textproc
MASTER_SITES=	${MASTER_SITE_SOURCEFORGE_JP}
MASTER_SITE_SUBDIR=	senna/46945

MAINTAINER=	kuriyama@FreeBSD.org
COMMENT=	Embeddable Fulltext Search Engine

GNU_CONFIGURE=	YES
USE_GCC=	any
USES=		gmake libtool
USE_LDCONFIG=	YES
CONFIGURE_ARGS=	--with-sennahome=${SENNA_HOME}
LDFLAGS+=	-L${LOCALBASE}/lib ${PTHREAD_LIBS}
MAKE_ARGS=	CFLAGS="${CFLAGS} -I${LOCALBASE}/include ${PTHREAD_CFLAGS}"
WRKSRC=		${WRKDIR}/${DISTNAME}

SENNA_HOME?=	/var/senna

OPTIONS_DEFINE=	MECAB NFKC
OPTIONS_DEFAULT=	MECAB NFKC
MECAB_DESC=	use mecab for morphological analysis
NFKC_DESC=	use nfkc based utf8 normalization

.include <bsd.port.options.mk>

.if ${ARCH} == "ia64" || ${ARCH} == "sparc64"
BROKEN=		Does not compile on ${ARCH}
.endif

.if ${PORT_OPTIONS:MMECAB}
CONFIGURE_ARGS+=	--with-mecab
LIB_DEPENDS+=	libmecab.so:${PORTSDIR}/japanese/mecab
.else
CONFIGURE_ARGS+=	--without-mecab
.endif

.if ${PORT_OPTIONS:MNFKC}
CONFIGURE_ARGS+=	--disable-nfkc
.endif

.include <bsd.port.mk>
