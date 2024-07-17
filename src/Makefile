SRCS := cache.c \
    dhcp.c \
    dnsmasq.c \
    forward.c \
    helper.c \
    lease.c \
    log.c \
    netlink.c \
    network.c \
    option.c \
    rfc1035.c \
    rfc2131.c \
    util.c

CFLAGS := -O2 -g -W -Wall -D__ANDROID__ -DIPV6 -DNO_SCRIPT \
    -D_BSD_SOURCE -Wno-unused-variable -Wno-unused-parameter

ifeq ($(FORCE_HARDCODED_CONFFILE), 1)
    CFLAGS += -DFORCE_HARDCODED_CONFFILE
else
    $(info #########################################)
    $(info Not using hardcoded config file, use FORCE_HARDCODED_CONFFILE=1 to force the use of config file and disable CLI)
    $(info #########################################)
endif

dnsmasq: $(SRCS)
	$(CC) $(CFLAGS) -llog -o $@ $^
	# Fix for Termux-based build env
	# Termux adds rpath by default pointing towards Termux's own
	# lib directory.
	# We don't want to trip SELinux at link-time by searching
	# that directory through rpath
	patchelf --remove-rpath $@

clean:
	rm dnsmasq
.PHONY: clean
