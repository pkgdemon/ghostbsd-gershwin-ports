PORTNAME=	libs-back
DISTVERSION=	20250615
CATEGORIES=	x11-toolkits gnustep
PKGNAMEPREFIX=	gershwin-

MAINTAINER=	jpm820@proton.me
COMMENT=	GNUstep GUI backend
WWW=		http://www.gnustep.org/

LICENSE=	GPLv3 LGPL3
LICENSE_COMB=	multi

LIB_DEPENDS+=	libgif.so:graphics/giflib \
		libtiff.so:graphics/tiff \
		libXft.so:x11-fonts/libXft \
		libfontconfig.so:x11-fonts/fontconfig \
		libfreetype.so:print/freetype2 \
		libcairo.so:graphics/cairo

USES=		gl gershwin jpeg pkgconfig xorg
CONFLICTS=	gnustep-back
USE_GERSHWIN=	base gui build
USE_XORG=	xft xrender xmu xext x11 xcursor xfixes xmu
USE_GL=	gl
USE_LDCONFIG=	${GNUSTEP_SYSTEM_LIBRARIES}

USE_GITHUB=	yes
GH_ACCOUNT=	gnustep
GH_TAGNAME= d277919

GNU_CONFIGURE=	yes
CONFIGURE_ARGS=	--enable-graphics=cairo \
		--disable-glitz

# LLD 7 creates a library that does not work with FreeBSD (or OpenBSD) rtld -
# it loads apparently without errors, but the global constructors are not
# called.  It also appears to corrupt some internal state, as throwing an
# exception causes a crash inside rtld.
LLD_UNSAFE=     yes

MAKE_FLAGS+=    OPTFLAG="${CFLAGS} -I${LOCALBASE}/include"
BACKVERSION=    ${PORTVERSION:C/([0-9])*[.]([0-9]*).*/\1\2/1}

CFLAGS+=        -I${LOCALBASE}/include/freetype2
PLIST_SUB+=     BACK=back-${BACKVERSION}
PLIST_SUB+=     BACKVERSION=${PORTVERSION:C/([0-9])*[.]([0-9]*).*/\1\2/1}

pre-configure:
.for file in config.guess config.sub install-sh
		 @${CP} ${GNUSTEP_PREFIX}/System/Library/Makefiles/${file} ${WRKSRC}
.endfor

.include <bsd.port.mk>
