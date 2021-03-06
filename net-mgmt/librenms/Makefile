# Created by: Muhammad Moinur Rahman<bofh@FreeBSD.org>
# $FreeBSD$

PORTNAME=	librenms
PORTVERSION=	1.48.1
PORTEPOCH=	1
CATEGORIES=	net-mgmt
MASTER_SITES=	LOCAL/dvl:vendor
DISTFILES=	${PORTNAME}-vendor-${DISTVERSIONPREFIX}${DISTVERSION}${DISTVERSIONSUFFIX}${EXTRACT_SUFX}:vendor

MAINTAINER=	dvl@FreeBSD.org
COMMENT=	Autodiscovering PHP/MySQL/SNMP based network monitoring

LICENSE=	GPLv3

USES=		python${PY_MYSQL} shebangfix

# RELEASE_TIMESTAMP is used for a patch inside the vendor code
# it represents the release date via: git show --pretty='%H|%ct' -s 1.42.01
# It sits here so you remember to update it with each release
RELEASE_TIMESTAMP=	1548881623

# perhaps we also need python-memcache python-mysqldb
RUN_DEPENDS+=	rrdtool:databases/rrdtool \
		dot:graphics/graphviz \
		${LOCALBASE}/share/pear/Net/IPv4.php:net/pear-Net_IPv4@${PHP_FLAVOR} \
		${LOCALBASE}/share/pear/Net/IPv6.php:net/pear-Net_IPv6@${PHP_FLAVOR} \
		snmpget:net-mgmt/net-snmp \
		bash:shells/bash \
		sudo:security/sudo

USE_PHP=	ctype curl filter gd hash json ldap mbstring mysqli openssl pdo pdo_mysql phar posix session simplexml snmp tokenizer xml zip

USE_GITHUB=	yes
GH_ACCOUNT=	librenms

USERS=		www
WWW_USER=	www

NO_BUILD=	yes

OPTIONS_DEFINE=	APACHEMOD FPING IPMITOOL LIBVIRT MYSQLD NAGPLUGINS NMAP PYPOLLER WMIC DOCS EXAMPLES X11
OPTIONS_DEFAULT=	APACHEMOD FPING IPMITOOL LIBVIRT NAGPLUGINS NMAP PYPOLLER WMIC
APACHEMOD_DESC=	Use PHP with Apache 2.2+ module
FPING_DESC=	Enable fping support ping monitoring
IPMITOOL_DESC=	Enable support for monitoring hardware IPMI
MYSQLD_DESC=	Use local MySQL server
WMIC_DESC=	Enable support for WMI polling
PYPOLLER_DESC=	Enable Python Poller Wrapper

FPING_RUN_DEPENDS=	fping:net/fping
IPMITOOL_RUN_DEPENDS=	ipmitool:sysutils/ipmitool
LIBVIRT_RUN_DEPENDS=	virsh:devel/libvirt
NAGPLUGINS_RUN_DEPENDS=	${LOCALBASE}/libexec/nagios/check_nagios:net-mgmt/nagios-plugins
NMAP_RUN_DEPENDS=	nmap:security/nmap
PYPOLLER_RUN_DEPENDS=	${PYTHON_PKGNAMEPREFIX}MySQLdb>=1.2.3:databases/py-MySQLdb@${PY_FLAVOR}
PYPOLLER_VARS=	PY_MYSQL=:2.7
X11_RUN_DEPENDS=	Magick-config:graphics/ImageMagick6 \
			mtr:net/mtr
X11_RUN_DEPENDS_OFF=	Magick-config:graphics/ImageMagick6-nox11 \
			mtr:net/mtr-nox11

WMIC_RUN_DEPENDS=	wmic:net-mgmt/wmi-client
MYSQLD_USES=		mysql:server
MYSQLD_USES_OFF=	mysql:client

SHEBANG_FILES=	scripts/auth_test.php scripts/deploy-docs.sh scripts/github-remove \
		scripts/Migration/Standard_Conversion/convert_no_xml.sh \
		scripts/Migration/Standard_Conversion/destwork_no_xml.sh \
		scripts/Migration/Standard_Conversion/mkdir.sh \
		scripts/Migration/XML_Conversion/convert.sh \
		scripts/Migration/XML_Conversion/destwork.sh \
		scripts/Migration/XML_Conversion/mkdir.sh \
		scripts/removespikes.pl scripts/removespikes.php scripts/watchmaillog/watchmaillog.pl \
		poller.php poller-wrapper.py \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/generate-includes.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/flush-definition-cache.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/old-remove-require-once.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/config-scanner.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/flush.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/add-vimline.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/remove-trailing-whitespace.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/merge-library.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/old-extract-schema.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/rename-config.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/generate-standalone.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/generate-schema-cache.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/old-remove-schema-def.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/generate-entity-file.php \
		../${PORTNAME}-vendor-${PORTVERSION}/ezyang/htmlpurifier/maintenance/update-config.php \
		../${PORTNAME}-vendor-${PORTVERSION}/swiftmailer/swiftmailer/lib/swiftmailer_generate_mimes_config.php \
		../${PORTNAME}-vendor-${PORTVERSION}/tecnickcom/tcpdf/tools/tcpdf_addfont.php

SUB_FILES+=	pkg-message
SUB_LIST+=	PHP="${PHPBASE}/bin/php" PYTHON=${PYTHON_CMD}

ROOT_FILES=	.env.example addhost.php adduser.php alerts.php artisan billing-calculate.php \
		build-base.php build.sql check-services.php composer.json \
		composer.lock config.php.default config_to_json.php cronic daily.php daily.sh \
		delhost.php discovery-wrapper.py discovery.php dist-pollers.php irc.php \
		librenms-service.py mkdocs.yml pbin.sh phpunit.xml ping.php poll-billing.php poller.php poller-service.py \
		poller-wrapper.py readmegen.yml renamehost.php services-wrapper.py snmp-scan.py \
		snmptrap.php syslog.php validate.php

ROOT_DIRS=	LibreNMS app bootstrap config contrib database doc html includes licenses logs mibs misc resources routes scripts sql-schema storage tests

# these are directories which require a generic @DIR entry in pkg-plist
OTHER_DIRS=	storage/app/public \
		storage/debugbar \
		storage/framework/testing \
		storage/logs \
		vendor/amenadiel/jpgraph/tests/_output \
		vendor/amenadiel/jpgraph/tests/_support/_generated \
		vendor/doctrine/common/lib/vendor/doctrine-build-common \
		vendor/doctrine/dbal/lib/vendor/Symfony/Component/Console \
		vendor/doctrine/dbal/lib/vendor/doctrine-build-common \
		vendor/doctrine/dbal/lib/vendor/doctrine-common \
		vendor/laravel/laravel/bootstrap/cache \
		vendor/laravel/laravel/storage/app/public \
		vendor/laravel/laravel/storage/framework/cache \
		vendor/laravel/laravel/storage/framework/sessions \
		vendor/laravel/laravel/storage/framework/testing \
		vendor/laravel/laravel/storage/framework/views \
		vendor/laravel/laravel/storage/logs

DOCS=		AUTHORS.md CHANGELOG.md CONTRIBUTING.md LICENSE.txt README.md
PORTDOCS=	*
PORTEXAMPLES=	snmp.conf.example snmpd.conf.example
NO_ARCH=	yes

APACHEMOD_USES=		php:mod
APACHEMOD_USES_OFF=	php:web

post-patch:
	@${REINPLACE_CMD}    's|%%PORTNAME%%|${PORTNAME}|g'                   ${WRKSRC}/config.php.default
	@${REINPLACE_CMD}    's|%%WWW_USER%%|${WWW_USER}|g'                   ${WRKSRC}/config.php.default
	@${REINPLACE_CMD}    's|%%LOCALBASE%%|${LOCALBASE}|g'                 ${WRKSRC}/poller-wrapper.py ${WRKSRC}/poller.php
	@${REINPLACE_CMD}    's|%%PORTVERSION%%|${PORTVERSION}|g'             ${WRKSRC}/includes/common.php
	@${REINPLACE_CMD}    's|%%RELEASE_TIMESTAMP%%|${RELEASE_TIMESTAMP}|g' ${WRKSRC}/includes/common.php
	@${REINPLACE_CMD} -e 's|/opt/librenms|${WWWDIR}|'                     ${WRKSRC}/html/install.php
	@${RM} ${WRKSRC}/LibreNMS/Validations/Updates.php

do-install:
	${MKDIR} ${STAGEDIR}/${WWWDIR}
.for dir in ${ROOT_DIRS}
	${MKDIR} ${STAGEDIR}/${WWWDIR}/${dir}
	(cd ${WRKSRC}/${dir} && ${COPYTREE_SHARE} . ${STAGEDIR}/${WWWDIR}/${dir})
.endfor
.for f in ${ROOT_FILES}
	${INSTALL_DATA} ${WRKSRC}/${f} ${STAGEDIR}/${WWWDIR}
.endfor
	${MKDIR} ${STAGEDIR}/${WWWDIR}/vendor
	(cd ${WRKDIR}/${PORTNAME}-vendor-${PORTVERSION} && ${COPYTREE_SHARE} . ${STAGEDIR}/${WWWDIR}/vendor)
# Make daily.sh executable
	${CHMOD} 0755 ${STAGEDIR}/${WWWDIR}/daily.sh
# Files in scripts dir should be executable
	${FIND} ${STAGEDIR}/${WWWDIR}/scripts -type f -exec ${CHMOD} +x {} \;
# Ensure PHP and Python scripts are executable
	${FIND} ${STAGEDIR}/${WWWDIR} -type f -name '*.py' -or -type f -name \
	       '*.php' -exec ${CHMOD} +x {} \;
# these values should be outside the www tree now
	${MKDIR} ${STAGEDIR}/var/log/${PORTNAME}
	${MKDIR} ${STAGEDIR}/var/db/${PORTNAME}

do-install-DOCS-on:
	${MKDIR} ${STAGEDIR}/${DOCSDIR}
.for f in ${DOCS}
	${INSTALL_DATA} ${WRKSRC}/${f} ${STAGEDIR}/${DOCSDIR}
.endfor
	cd ${WRKSRC}/doc && ${COPYTREE_SHARE} . ${STAGEDIR}/${DOCSDIR}

do-install-EXAMPLES-on:
	${MKDIR} ${STAGEDIR}/${EXAMPLESDIR}
.for f in ${PORTEXAMPLES}
	${INSTALL_DATA} ${WRKSRC}/${f} ${STAGEDIR}/${EXAMPLESDIR}
.endfor

post-install:
	@${FIND} -s ${STAGEDIR}${WWWDIR} -type f '(' -name '*.orig' -or -name '*.bak' -or -name '.gitignore' ')' -delete
	@${FIND} -s ${STAGEDIR}${WWWDIR} -not -type d | ${SORT} | \
		${SED} -e 's#^${STAGEDIR}${PREFIX}/##' >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(www,www,0775) ${WWWDIR}/logs" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(www,www,0775) ${WWWDIR}/bootstrap/cache" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(www,www,0775) ${WWWDIR}/storage" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(www,www,0775) ${WWWDIR}/storage/framework/cache" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(www,www,0775) ${WWWDIR}/storage/framework/sessions" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(www,www,0775) ${WWWDIR}/storage/framework/views" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(www,www,0775) /var/log/${PORTNAME}" >> ${TMPPLIST}
	@${ECHO_CMD} "@dir(www,www,0775) /var/db/${PORTNAME}" >> ${TMPPLIST}
.for f in ${OTHER_DIRS}
	@${ECHO_CMD} "@dir(root,www,0775) ${WWWDIR}/${f}" >> ${TMPPLIST}
.endfor

.include <bsd.port.mk>
