#!/usr/bin/make -f
# file: plc/Makefile

# ====================================================================
# environment definitions;
# --------------------------------------------------------------------

include ../make.def

# ====================================================================
# symbols;
# --------------------------------------------------------------------

CFLAGS+=
LDFLAGS+=
TRASH=*.o *.obj *.exe t t.* *~ *.[0-9][0-9][0-9]
FILES=Makefile *.mak *.sh *.txt *.c
TOOLS=plcsnif
PAGES=plcsnif.1

# ====================================================================
# pseudo targets;
# --------------------------------------------------------------------

all compile: ${TOOLS}
compact: compile
	if [ ! -z ${STRIP} ]; then ${STRIP} ${TOOLS}; fi
	if [ -x /usr/local/bin/upx ]; then upx --best ${TOOLS}; fi
library:
	install -m ${DIR_PERM} -o ${OWNER} -g ${GROUP} -d ${BIN}
scripts:
manuals:
	test -d ${MAN} || install -m ${DIR_PERM} -o ${OWNER} -g ${GROUP} -d ${MAN}
	install -m ${MAN_PERM} -o ${OWNER} -g ${GROUP} ${PAGES} ${MAN}
install: $(TOOLS) library
	install -m ${SUID_PERM} -o ${OWNER} -g ${GROUP} ${TOOLS} ${BIN}
uninstall:
	cd ${BIN}; rm -f ${TOOLS}
	cd ${MAN}; rm -f ${PAGES}
check:
	${SHELL} plc.sh
fresh: clean compile
clean:
	rm -f ${TRASH} ${TOOLS}
ignore:
	echo ${TOOLS} | tr ' ' '\n' > .gitignore

# ====================================================================
# programs;
# --------------------------------------------------------------------

%: %.o
	${CC} -o ${@} ${^} ${LDFLAGS}
%.o: %.c
	${CC} -c ${<} ${CFLAGS}

# ====================================================================
# programs;
# --------------------------------------------------------------------
plcsnif: plcsnif.o chipset.o Devices.o Confirm.o Display.o Failure.o Request.o ReadMME.o SendMME.o getoptv.o putoptv.o version.o uintspec.o hexdump.o hexdecode.o hexencode.o hexstring.o hexout.o todigit.o synonym.o error.o typename.o initchannel.o openchannel.o closechannel.o readpacket.o sendpacket.o channel.o MMECode.o EthernetHeader.o QualcommHeader.o UnwantedMessage.o Sniffer.o Monitor.o
# ====================================================================
# includes;
# --------------------------------------------------------------------

include ../tools/tools.mak
include ../ether/ether.mak
include ../nodes/nodes.mak
include ../ram/ram.mak
include ../pib/pib.mak
include ../nvm/nvm.mak
include ../mme/mme.mak
include ../key/key.mak
include ../plc/plc.mak

