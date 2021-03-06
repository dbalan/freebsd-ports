# $FreeBSD$

PORTNAME=	ncbi-blast+
DISTVERSION=	2.8.1
PORTREVISION=	1
CATEGORIES=	biology perl5 python
MASTER_SITES=	https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/ \
		https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/${PORTVERSION}/
DISTNAME=	ncbi-blast-${PORTVERSION}+-src

MAINTAINER=	jwb@FreeBSD.org
COMMENT=	NCBI implementation of Basic Local Alignment Search Tool

LICENSE=	PD
LICENSE_FILE=	${WRKSRC}/scripts/projects/blast/LICENSE

BROKEN_powerpc64=	fails to build: Error 2

LIB_DEPENDS=	libpcre.so:devel/pcre \
		liblmdb.so:databases/lmdb \
		liblzo2.so:archivers/lzo2 \
		libgnutls.so:security/gnutls \
		libtspi.so:security/trousers \
		libgmp.so:math/gmp \
		libidn2.so:dns/libidn2 \
		libnettle.so:security/nettle \
		libhogweed.so:security/nettle \
		libtasn1.so:security/libtasn1 \
		libp11-kit.so:security/p11-kit \
		libgcrypt.so:security/libgcrypt \
		libgpg-error.so:security/libgpg-error \
		libsqlite3.so:databases/sqlite3
RUN_DEPENDS=	p5-List-MoreUtils>=0:lang/p5-List-MoreUtils

USES=		compiler:openmp gmake shebangfix perl5 python
USE_LDCONFIG=	yes

SHEBANG_FILES=	src/app/blast/legacy_blast.pl \
		src/app/blast/update_blastdb.pl \
		src/app/winmasker/windowmasker_2.2.22_adapter.py \
		src/app/blast/get_species_taxids.sh
GNU_CONFIGURE=	yes

# configure chooses /usr/local/bin/ar with no flags
# FreeBSD boost port flagged by configure as untested version
# --libdir=${PREFIX}/lib/ncbi-tools++ doesn't respect DESTDIR, so do
# a postinstall mv.
CONFIGURE_ARGS=	AR="ar cr" --without-boost --libdir=${PREFIX}/lib/ncbi-tools++

WRKSRC_SUBDIR=		c++

post-install:
	@${RM} ${STAGEDIR}${PREFIX}/include/ncbi-tools++/*/*/.cvsignore.extra
	@${RM} -rf ${STAGEDIR}${PREFIX}/lib/X11
	@${RMDIR} ${STAGEDIR}${PREFIX}/lib/debug
	${STRIP_CMD} ${STAGEDIR}${PREFIX}/lib/ncbi-tools++/*.so

.include <bsd.port.mk>
