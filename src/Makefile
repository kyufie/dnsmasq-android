OBJS := cache.o \
    dhcp.o \
    dnsmasq.o \
    forward.o \
    helper.o \
    lease.o \
    log.o \
    netlink.o \
    network.o \
    option.o \
    rfc1035.o \
    rfc2131.o \
    util.o

CFLAGS := -O2 -g -W -Wall -D__ANDROID__ -DIPV6 -DNO_SCRIPT \
    -D_BSD_SOURCE -Wno-unused-variable -Wno-unused-parameter

ifeq ($(FORCE_HARDCODED_CONFFILE), 1)
    CFLAGS += -DFORCE_HARDCODED_CONFFILE
else
    $(info #########################################)
    $(info Not using hardcoded config file, use FORCE_HARDCODED_CONFFILE=1 to force the use of config file and disable CLI)
    $(info #########################################)
endif

# Note for Termux-based build env
# Termux adds rpath by default, pointing towards Termux's own
# lib directory.
# We don't want to trip SELinux at link-time by making
# the linker search through that directory.
dnsmasq: $(OBJS)
	$(CC) $(CFLAGS) -llog -o $@ $^
	command -v patchelf > /dev/null && patchelf --remove-rpath $@

clean:
	rm $(OBJS) dnsmasq
.PHONY: clean
