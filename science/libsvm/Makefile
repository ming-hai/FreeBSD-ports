# Created by: Chia-Hsing Yu <me@davidyu.org>
# $FreeBSD$

PORTNAME=	libsvm
PORTVERSION=	3.21
CATEGORIES=	science math
MASTER_SITES=	http://www.csie.ntu.edu.tw/~cjlin/libsvm/ \
		http://www.csie.ntu.edu.tw/~cjlin/libsvm/oldfiles/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Library for Support Vector Machines

LICENSE=	BSD3CLAUSE
LICENSE_FILE=	${WRKSRC}/COPYRIGHT

OPTIONS_DEFINE=	OPTIMIZED_CFLAGS DOCS
OPTIONS_DEFAULT=	OPTIMIZED_CFLAGS

USES=		zip

USE_LDCONFIG=	yes
ALL_TARGET=	all lib

.if defined(PKGNAMESUFFIX) && ${PKGNAMESUFFIX} == "-python"
CATEGORIES+=	python

USES+=		python

MAKE_ARGS=	PYTHON_INCLUDEDIR=${PYTHON_INCLUDEDIR}

TXT_DOCS=	README.python

NO_BUILD=	yes

.else
TXT_DOCS=	COPYRIGHT README FAQ.html README.tools

TOOLS=		tools/checkdata.py tools/easy.py tools/grid.py tools/subset.py

SUB_FILES=	pkg-message
SUB_LIST=	DATADIR=${DATADIR}

.endif

.include <bsd.port.pre.mk>

.if ${PORT_OPTIONS:MDOCS}
PORTDOCS=	${TXT_DOCS}
.endif

.if ${PORT_OPTIONS:MOCFLAGS}
# same as LIBSVM itself
CFLAGS=		-Wall -Wconversion -O3
.endif

post-patch:
.if defined(PKGNAMESUFFIX) && ${PKGNAMESUFFIX} == "-python"
	@${CP} ${WRKSRC}/python/README ${WRKSRC}/README.python
.else
	@${CP} ${WRKSRC}/tools/README ${WRKSRC}/README.tools
.endif

.if defined(PKGNAMESUFFIX) && ${PKGNAMESUFFIX} == "-python"
do-install:
	${MKDIR} ${STAGEDIR}${PYTHON_SITELIBDIR}
	${INSTALL_DATA} ${WRKSRC}/python/svm.py ${STAGEDIR}${PYTHON_SITELIBDIR}
	${INSTALL_DATA} ${WRKSRC}/python/svmutil.py ${STAGEDIR}${PYTHON_SITELIBDIR}
.else

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/svm-train ${STAGEDIR}${PREFIX}/bin/
	${INSTALL_PROGRAM} ${WRKSRC}/svm-predict ${STAGEDIR}${PREFIX}/bin/
	${INSTALL_PROGRAM} ${WRKSRC}/svm-scale ${STAGEDIR}${PREFIX}/bin/
	${INSTALL_DATA} ${WRKSRC}/svm.h ${STAGEDIR}${PREFIX}/include/
	${INSTALL_LIB} ${WRKSRC}/libsvm.so.2 ${STAGEDIR}${PREFIX}/lib/
	${LN} -sf libsvm.so.2 ${STAGEDIR}${PREFIX}/lib/libsvm.so
	${MKDIR} ${STAGEDIR}${DATADIR}
	for f in ${TOOLS}; do \
	  ${INSTALL_DATA} ${WRKSRC}/$$f ${STAGEDIR}${DATADIR}; \
	done

.endif

post-install-DOCS-on:
	@${MKDIR} ${STAGEDIR}${DOCSDIR}
	for f in ${TXT_DOCS}; do \
	  ${INSTALL_DATA} ${WRKSRC}/$$f ${STAGEDIR}${DOCSDIR}; \
	done

.include <bsd.port.post.mk>
