# Created by: Antoine Brodin <antoine@FreeBSD.org>
# $FreeBSD$

PORTNAME=	dfwinreg
PORTVERSION=	20190122
CATEGORIES=	security devel python
MASTER_SITES=	CHEESESHOP \
		https://github.com/log2timeline/dfwinreg/releases/download/${PORTVERSION}/
PKGNAMEPREFIX=	${PYTHON_PKGNAMEPREFIX}

MAINTAINER=	antoine@FreeBSD.org
COMMENT=	Digital Forensics Windows Registry

LICENSE=	APACHE20
LICENSE_FILE=	${WRKSRC}/LICENSE

RUN_DEPENDS=	libregf>=a:devel/libregf \
		${PYTHON_PKGNAMEPREFIX}dtfabric>=0:devel/py-dtfabric@${PY_FLAVOR} \
		${PYTHON_PKGNAMEPREFIX}dfdatetime>=0:security/py-dfdatetime@${PY_FLAVOR}
TEST_DEPENDS=	${PYTHON_PKGNAMEPREFIX}mock>0:devel/py-mock@${PY_FLAVOR}

NO_ARCH=	yes
USES=		python
USE_PYTHON=	distutils autoplist concurrent

post-patch:
	${REINPLACE_CMD} "s,share/doc/dfwinreg,${DOCSDIR_REL}," ${WRKSRC}/setup.py

do-test:
	@(cd ${TEST_WRKSRC} && ${SETENV} ${TEST_ENV} ${PYTHON_CMD} run_tests.py)

.include <bsd.port.mk>
