# Created by: Alexey Dokuchaev <danfe@FreeBSD.org>
# $FreeBSD$

PORTNAME=	nexuiz
PORTVERSION=	2.5.2
PORTREVISION=	15
CATEGORIES=	games
MASTER_SITES=	SF/${PORTNAME}/NexuizRelease/Nexuiz%20${PORTVERSION} \
		SF/${PORTNAME}/mappack/nexmappack_r2:mappack
DISTNAME=	${PORTNAME}-${PORTVERSION:S/.//g}
DISTFILES=	${DISTNAME}${EXTRACT_SUFX}

MAINTAINER=	amdmi3@FreeBSD.org
COMMENT=	Fast-paced, chaotic, and intense multiplayer first person shooter

LIB_DEPENDS=	libcurl.so:${PORTSDIR}/ftp/curl \
		libjpeg.so:${PORTSDIR}/graphics/jpeg

LICENSE=	GPLv2

MANUAL_PACKAGE_BUILD=   huge

USES=		zip:infozip
WRKSRC=		${WRKDIR}/Nexuiz/sources/darkplaces
MAKEFILE=	BSDmakefile
MAKE_ARGS=	DP_FS_BASEDIR="${DATADIR}" CC="${CC}" \
		DP_PRELOAD_DEPENDENCIES=yes DP_LINK_TO_LIBJPEG=yes \
		CFLAGS_LIBJPEG="-I${LOCALBASE}/include" \
		OPTIM_RELEASE="${CFLAGS} -fno-strict-aliasing -funroll-loops" \
		STRIP="${STRIP_CMD}"
MAKE_JOBS_UNSAFE=yes
ALL_TARGET=	# empty

PORTDATA=	*

OPTIONS_DEFINE=	MAPPACK
OPTIONS_MULTI=	COMPONENTS
OPTIONS_MULTI_COMPONENTS=CLIENT SDL_CLIENT DEDICATED
OPTIONS_DEFAULT=MAPPACK CLIENT SDL_CLIENT DEDICATED

MAPPACK_DESC=	Install community map pack
CLIENT_DESC=	Build GLX client
SDL_CLIENT_DESC=Build SDL client
DEDICATED_DESC=	Build dedicated server

CLIENT_LIB_DEPENDS=	libmodplug.so:${PORTSDIR}/audio/libmodplug \
			libpng.so:${PORTSDIR}/graphics/png \
			libtheora.so:${PORTSDIR}/multimedia/libtheora
SDL_CLIENT_LIB_DEPENDS=	${CLIENT_LIB_DEPENDS}
MAPPACK_DISTFILES=	nexmappack_r2${EXTRACT_SUFX}:mappack

.include <bsd.port.options.mk>

.if ${PORT_OPTIONS:MCLIENT}
USE_GL=		glut
USE_XORG=	x11 xpm xxf86vm xxf86dga xext
ALL_TARGET+=	cl-release
PLIST_FILES+=	bin/${PORTNAME}-glx

DESKTOP_ENTRIES="Nexuiz" \
		"${COMMENT}" \
		"${PREFIX}/share/pixmaps/${PORTNAME}.ico" \
		"${PORTNAME}-glx" \
		"Game;Shooter;" \
		""
.endif

.if ${PORT_OPTIONS:MSDL_CLIENT}
USE_SDL=	sdl
ALL_TARGET+=	sdl-release
PLIST_FILES+=	bin/${PORTNAME}-sdl

# override of DESKTOP_ENTRIES for GLX client is intented
DESKTOP_ENTRIES="Nexuiz" \
		"${COMMENT}" \
		"${PREFIX}/share/pixmaps/${PORTNAME}.ico" \
		"${PORTNAME}-sdl" \
		"Game;Shooter;" \
		""
.endif

.if ${PORT_OPTIONS:MCLIENT} || ${PORT_OPTIONS:MSDL_CLIENT}
PLIST_FILES+=	share/pixmaps/${PORTNAME}.ico
.endif

.if ${PORT_OPTIONS:MDEDICATED}
ALL_TARGET+=	sv-release
PLIST_FILES+=	bin/${PORTNAME}-dedicated
.endif

post-extract:
	@${EXTRACT_CMD} -qo \
		${WRKDIR}/Nexuiz/sources/enginesource20091001.zip \
		-d ${WRKDIR}/Nexuiz/sources

post-patch:
	@${REINPLACE_CMD} -e 's,/usr/X11R6,${LOCALBASE},' \
		${WRKSRC}/${MAKEFILE} ${WRKSRC}/makefile.inc
	@${REINPLACE_CMD} -e '/LDFLAGS_BSDSV/s,$$,-L${LOCALBASE}/lib,' \
		${WRKSRC}/makefile.inc
# Fix for libpng 1.4
	@${REINPLACE_CMD} -e 's,gray_1_2_4_to_8,expand_&,g' \
		${WRKSRC}/image_png.c

do-install:
.if ${PORT_OPTIONS:MCLIENT}
	${INSTALL_PROGRAM} ${WRKDIR}/Nexuiz/sources/darkplaces/darkplaces-glx ${STAGEDIR}${PREFIX}/bin/${PORTNAME}-glx
.endif
.if ${PORT_OPTIONS:MSDL_CLIENT}
	${INSTALL_PROGRAM} ${WRKDIR}/Nexuiz/sources/darkplaces/darkplaces-sdl ${STAGEDIR}${PREFIX}/bin/${PORTNAME}-sdl
.endif
.if ${PORT_OPTIONS:MCLIENT} || ${PORT_OPTIONS:MSDL_CLIENT}
	${INSTALL_DATA} ${WRKDIR}/Nexuiz/sources/darkplaces/nexuiz.ico ${STAGEDIR}${PREFIX}/share/pixmaps
.endif
.if ${PORT_OPTIONS:MDEDICATED}
	${INSTALL_PROGRAM} ${WRKDIR}/Nexuiz/sources/darkplaces/darkplaces-dedicated ${STAGEDIR}${PREFIX}/bin/${PORTNAME}-dedicated
	cd ${WRKDIR}/Nexuiz && ${COPYTREE_SHARE} "server" ${STAGEDIR}${DATADIR}
# Fixup lost +x permissions on scripts after COPYTREE_SHARE
	${FIND} ${STAGEDIR}${DATADIR}/server -type f -name *.sh -o -name rcon*.pl | \
		${XARGS} ${CHMOD} +x
.endif
	cd ${WRKDIR}/Nexuiz && ${COPYTREE_SHARE} "data havoc" ${STAGEDIR}${DATADIR}
.if ${PORT_OPTIONS:MMAPPACK}
	${INSTALL_DATA} ${WRKDIR}/data/*.pk3 ${STAGEDIR}${DATADIR}/data
.endif

.include <bsd.port.mk>
