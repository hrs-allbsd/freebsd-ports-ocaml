# Created by: Goran Lowkrantz <glz@hidden-powers.com>
# $FreeBSD$

PORTNAME=	piwigo
DISTVERSION=	2.9.4
PORTREVISION=	2
CATEGORIES=	www
MASTER_SITES=	https://piwigo.org/download/dlcounter.php?code=${PORTVERSION}&/

MAINTAINER=	tremere@cainites.net
COMMENT=	PHP based Web Gallery

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/doc/COPYING

NO_BUILD=	yes
NO_ARCH=	yes
USES=		cpe php:web zip
USE_PHP=	calendar ctype dom exif filter gd gettext hash iconv json \
		mbstring mcrypt mysqli openssl pcre pdf pdo posix \
		session simplexml sockets spl tokenizer xml xmlreader \
		xmlwriter zlib
WRKSRC=		${WRKDIR}/${PORTNAME}

SUB_FILES=	pkg-deinstall pkg-message
SUB_LIST+=	CP="${CP}" \
		MKDIR="${MKDIR}" \
		CHOWN="${CHOWN}" \
		TOUCH="${TOUCH}" \
		WWWOWN="${WWWOWN}" \
		WWWGRP="${WWWGRP}"

OPTIONS_DEFINE=	IMAGICK X11 DOCS EXAMPLES
OPTIONS_DEFAULT=IMAGICK
IMAGICK_DESC=	${IMAGEMAGICK_DESC}

PORTDOCS=	README_ca.txt README_en.txt README_fr.txt

PLIST_SUB+=	WWWOWN="${WWWOWN}" \
		WWWGRP="${WWWGRP}" \
		CHOWN="${CHOWN}"

.include <bsd.port.pre.mk>

.if ${PORT_OPTIONS:MIMAGICK}
.if ${PORT_OPTIONS:MX11}
RUN_DEPENDS+=	${LOCALBASE}/bin/convert:graphics/ImageMagick6
.else
RUN_DEPENDS+=	${LOCALBASE}/bin/convert:graphics/ImageMagick6-nox11
.endif
.endif

pre-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}/
	@cd ${WRKSRC}/doc/ && ${INSTALL_DATA} ${PORTDOCS} ${STAGEDIR}${DOCSDIR}/

pre-install-EXAMPLES-on:
	@${MKDIR} ${STAGEDIR}${EXAMPLESDIR}/
	@cd ${WRKSRC}/tools/ && ${COPYTREE_SHARE} . ${STAGEDIR}${EXAMPLESDIR}/

do-install:
	@cd ${WRKSRC}/doc/ && ${RM} ${PORTDOCS}
	@${RM} -r ${WRKSRC}/tools ${WRKSRC}/_data/dummy.txt
	@${INSTALL} -d ${STAGEDIR}${WWWDIR}
	@${TAR} -C ${WRKSRC} -cf - . | \
	${TAR} --unlink -C ${STAGEDIR}${WWWDIR} -xf -

.include <bsd.port.post.mk>
