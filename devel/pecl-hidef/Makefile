# Created by: chinsan
# $FreeBSD$

PORTNAME=	hidef
PORTVERSION=	0.1.13
PORTREVISION=	1
CATEGORIES=	devel pear
MASTER_SITES=	http://pecl.php.net/get/
PKGNAMEPREFIX=	pecl-
DIST_SUBDIR=	PECL

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Constants for real

DEPRECATED=	Works only with EOL php 5.5
EXPIRATION_DATE=	2016-10-20

LICENSE=	PHP301

USES=		php:ext tar:tgz
IGNORE_WITH_PHP=	56 70

CONFIGURE_ARGS=	--enable-hidef

CFLAGS+=	-I${LOCALBASE}/include
LDFLAGS+=	-L${LOCALBASE}/lib

post-patch:
	@${REINPLACE_CMD} -e 's,malloc.h,stdlib.h,g' \
	${WRKSRC}/hidef.c

.include <bsd.port.mk>
