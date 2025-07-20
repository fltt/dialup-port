PORTNAME=	dialup
DISTVERSION=	1.0.1
CATEGORIES=	net-mgmt sysutils
DISTFILES=

MAINTAINER=	franz.lattanzio@gmail.com
COMMENT=	Utilities to manage GSM/UMTS/LTE network adapters
WWW=		https://github.com/fltt/dialup-port/

LICENSE=	MIT
LICENSE_FILE=	${FILESDIR}/COPYING

RUN_DEPENDS=	dmenu:x11/dmenu \
		sudo:security/sudo

NO_ARCH=	yes
NO_BUILD=	yes
SUB_FILES=	${BIN_SCRIPTS:S/^/bin_/} ${DEVD_SCRIPTS:S/^/devd_/} \
		${DIAL_SCRIPTS:S/^/dial_/} ${EXAMPLES_DATA_SUB:S/^/examples_/} \
		${EXAMPLES_SCRIPTS:S/^/examples_/} \
		${PPP_DRIVER_SCRIPTS:S/^/drivers_ppp_/} \
		${SAMPLES_DEVD_DATA:S/^/samples_devd_/} \
		${SAMPLES_DIALUP_SCRIPTS:S/^/samples_dialup_/} config \
		pkg-message README samples_newsyslog.conf samples_sudoers \
		samples_syslog.conf
SUB_LIST=	LIBEXECDIR=${LIBEXECDIR} \
		PORTNAME=${PORTNAME}

PLIST_SUB=	LIBEXECDIR=${LIBEXECDIR} \
		PORTNAME=${PORTNAME}

OPTIONS_DEFINE=	DLINKCONTROL
OPTIONS_SUB=	yes

DLINKCONTROL_DESC=		Install the D-Link DWM-222 driver
DLINKCONTROL_RUN_DEPENDS=	dlinkcontrol:net-mgmt/dlinkcontrol
DLINKCONTROL_SUB_FILES=		${DLINK_DRIVER_SCRIPTS:S/^/drivers_dlink_/} \
				samples_devd_dlink.conf

BIN_SCRIPTS=	dialup hangup sync_sim

DEVD_SCRIPTS=	attach_u3g attach_ue attach_umodem detach_cua detach_ue \
		disable_sim eject enable_sim

DIAL_SCRIPTS=	check_availability monitor select_sim

DLINK_DRIVER_SCRIPTS=	connect disconnect get_iccid sm_read sm_write \
			unlock_sim

EXAMPLES_DATA_PLAIN=	ppp.linkdown ppp.linkup
EXAMPLES_DATA_SUB=	ppp.conf README
EXAMPLES_SCRIPTS=	linkup

LIBEXECDIR=	${PREFIX}/libexec/${PORTNAME}

PPP_DRIVER_DATA=	config
PPP_DRIVER_SCRIPTS=	connect disconnect get_iccid monitor sm_read sm_write \
			unlock_sim

SAMPLES_DEVD_DATA=	cd.conf cua.conf huawei.conf ue.conf

SAMPLES_DIALUP_DATA=	pins profiles
SAMPLES_DIALUP_SCRIPTS=	linkdown linkup

do-install:
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/devd
	for f in ${SAMPLES_DEVD_DATA}; \
		do ${INSTALL_DATA} ${WRKDIR}/samples_devd_$$f ${STAGEDIR}${PREFIX}/etc/devd/$$f.sample; \
		done
	${MKDIR} ${STAGEDIR}${ETCDIR}
	for f in ${SAMPLES_DIALUP_DATA}; \
		do ${INSTALL_DATA} ${FILESDIR}/samples_dialup_$$f ${STAGEDIR}${ETCDIR}/$$f.sample; \
		done
	for f in ${SAMPLES_DIALUP_SCRIPTS}; \
		do ${INSTALL_SCRIPT} ${WRKDIR}/samples_dialup_$$f ${STAGEDIR}${ETCDIR}/$$f.sample; \
		done
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/newsyslog.conf.d
	${INSTALL_DATA} ${WRKDIR}/samples_newsyslog.conf \
		${STAGEDIR}${PREFIX}/etc/newsyslog.conf.d/${PORTNAME}.conf.sample
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/sudoers.d
	${INSTALL_DATA} ${WRKDIR}/samples_sudoers \
		${STAGEDIR}${PREFIX}/etc/sudoers.d/${PORTNAME}.sample
	${MKDIR} ${STAGEDIR}${PREFIX}/etc/syslog.d
	${INSTALL_DATA} ${WRKDIR}/samples_syslog.conf \
		${STAGEDIR}${PREFIX}/etc/syslog.d/${PORTNAME}.conf.sample
	${MKDIR} ${STAGEDIR}${PREFIX}/bin
	for f in ${BIN_SCRIPTS}; \
		do ${INSTALL_SCRIPT} ${WRKDIR}/bin_$$f ${STAGEDIR}${PREFIX}/bin/$$f; \
		done
	${MKDIR} ${STAGEDIR}${LIBEXECDIR}
	${INSTALL_DATA} ${WRKDIR}/config \
		${STAGEDIR}${LIBEXECDIR}
	${MKDIR} ${STAGEDIR}${LIBEXECDIR}/devd
	for f in ${DEVD_SCRIPTS}; \
		do ${INSTALL_SCRIPT} ${WRKDIR}/devd_$$f ${STAGEDIR}${LIBEXECDIR}/devd/$$f; \
		done
	${MKDIR} ${STAGEDIR}${LIBEXECDIR}/dial
	for f in ${DIAL_SCRIPTS}; \
		do ${INSTALL_SCRIPT} ${WRKDIR}/dial_$$f ${STAGEDIR}${LIBEXECDIR}/dial/$$f; \
		done
	${MKDIR} ${STAGEDIR}${LIBEXECDIR}/drivers/ppp
	for f in ${PPP_DRIVER_DATA}; \
		do ${INSTALL_DATA} ${FILESDIR}/drivers_ppp_$$f ${STAGEDIR}${LIBEXECDIR}/drivers/ppp/$$f; \
		done
	for f in ${PPP_DRIVER_SCRIPTS}; \
		do ${INSTALL_SCRIPT} ${WRKDIR}/drivers_ppp_$$f ${STAGEDIR}${LIBEXECDIR}/drivers/ppp/$$f; \
		done
	${MKDIR} ${STAGEDIR}${DOCSDIR}
	${INSTALL_DATA} ${WRKDIR}/README \
		${STAGEDIR}${DOCSDIR}
	${MKDIR} ${STAGEDIR}${EXAMPLESDIR}
	for f in ${EXAMPLES_DATA_PLAIN}; \
		do ${INSTALL_DATA} ${FILESDIR}/examples_$$f ${STAGEDIR}${EXAMPLESDIR}/$$f; \
		done
	for f in ${EXAMPLES_DATA_SUB} ${EXAMPLES_SCRIPTS}; \
		do ${INSTALL_SCRIPT} ${WRKDIR}/examples_$$f ${STAGEDIR}${EXAMPLESDIR}/$$f; \
		done
	${MKDIR} ${STAGEDIR}/var/db/${PORTNAME}
	${MKDIR} ${STAGEDIR}/var/run/${PORTNAME}

do-install-DLINKCONTROL-on:
	${INSTALL_DATA} ${WRKDIR}/samples_devd_dlink.conf \
		${STAGEDIR}${PREFIX}/etc/devd/dlink.conf.sample
	${MKDIR} ${STAGEDIR}${LIBEXECDIR}/drivers/dlink
	for f in ${DLINK_DRIVER_SCRIPTS}; \
		do ${INSTALL_SCRIPT} ${WRKDIR}/drivers_dlink_$$f ${STAGEDIR}${LIBEXECDIR}/drivers/dlink/$$f; \
		done

.include <bsd.port.mk>
