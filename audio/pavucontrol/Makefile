# Created by: Romain Tartière <romain@blogreen.org>
# $FreeBSD$

PORTNAME=	pavucontrol
PORTVERSION=	3.0
PORTREVISION=	4
CATEGORIES=	audio
MASTER_SITES=	http://freedesktop.org/software/pulseaudio/${PORTNAME}/

MAINTAINER=	romain@FreeBSD.org
COMMENT=	GTK mixer for PulseAudio

LICENSE=	GPLv2
LICENSE_FILE=	${WRKSRC}/LICENSE

LIB_DEPENDS=	libpulse.so:audio/pulseaudio \
		libcanberra-gtk3.so:audio/libcanberra-gtk3

GNU_CONFIGURE=	yes
USES=		gmake pkgconfig gettext tar:xz compiler:c++11-lang
USE_GNOME=	glibmm gtkmm30 intltool libsigc++20
USE_CXXSTD=	c++11

CONFIGURE_ARGS=	--disable-lynx

post-patch:
# Install locales files in right place
	${REINPLACE_CMD} -e 's|[$$][(]DATADIRNAME[)]|share|' \
		${WRKSRC}/po/Makefile.in.in

.include <bsd.port.mk>
