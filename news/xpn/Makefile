# Created by: Nicola Vitale <nivit@FreeBSD.org>
# $FreeBSD$

PORTNAME=	xpn
PORTVERSION=	1.2.6
PORTREVISION=	7
CATEGORIES=	news python
MASTER_SITES=	http://xpn.altervista.org/codice/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	X Python Newsreader

LICENSE=	GPLv2

RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}gtk2>=2.24.0:x11-toolkits/py-gtk2@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}sqlite3>=2.7.9:databases/py-sqlite3@${PY_FLAVOR}

NO_ARCH=	yes
NO_BUILD=	yes

SHEBANG_FILES=	${XPN}
SUB_FILES=	${PORTNAME}
SUB_LIST=	PYTHON_CMD=${PYTHON_CMD} XPN=${XPN}

USES=		gettext python:2.7 shebangfix

XPN=	${PORTNAME}.py

OPTIONS_DEFINE=	DOCS

do-install:
	${MKDIR} ${STAGEDIR}${DATADIR}
	${INSTALL_SCRIPT} ${WRKSRC}/${XPN} ${STAGEDIR}${DATADIR}/${XPN}
	${INSTALL_SCRIPT} ${WRKDIR}/${PORTNAME} ${STAGEDIR}${PREFIX}/bin/${PORTNAME}
	(cd ${WRKSRC} && \
	${COPYTREE_SHARE} . ${STAGEDIR}${DATADIR} "-mindepth 2")
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKSRC}/${PORTNAME}.html ${STAGEDIR}${DOCSDIR}

.include <bsd.port.mk>
