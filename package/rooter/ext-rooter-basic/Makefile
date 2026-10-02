#Owned by DairyMan@Whirlpool
#
#Copyright GNU act.
include $(TOPDIR)/rules.mk

PKG_NAME:=ext-rooter-basic
PKG_VERSION:=4.500
# r10: /etc/hotplug.d/iface/50-z8102-wan6-mwan3 generalized to every enabled
# ipv6 mwan3 member, with withdrawal handling. Bumped because the package
# gains a new installed file -- without this the ipk keeps the same version
# with different contents and opkg will not upgrade an existing install.
# r11: two changes to /etc/hotplug.d/iface/50-z8102-wan6-mwan3, both needed.
#   (1) It no longer restarts mwan3 on an ipv6 rotation. The restart was global
#       (this mwan3 has no per-member restart, and reload == stop; start), so it
#       reset every member to its initial_state and put the ipv4 legs offline
#       for ~50s -- an ipv6 event breaking ipv4. The tracker re-derives its own
#       source (refresh_src_ip), so the hotplug now only records the change, and
#       only ever cycles an interface on withdrawal.
#   (2) The ACTION gate was widened from ACTION=ifupdate alone to
#       ifup|connected|ifupdate. ifupdate is real (netifd emitted it twice for
#       wan2_6 during a live rotation on 2026-10-02) but it only ever fires on a
#       ROTATION. A WITHDRAWAL -- interface up, global address gone, the actual
#       outage -- emits ifdown->ifup->connected and NO ifupdate, so the old gate
#       saw nothing and the withdrawal branch was unreachable. ifdown and
#       disconnected stay excluded: the withdrawal branch cycles the interface
#       back UP, so reacting to a way-down event would fight a shutdown.
# Bumped because the installed file changed contents and opkg will not upgrade
# an existing install at the same version.
PKG_RELEASE:=11

PKG_MAINTAINER:=Created by DM/makefile by Cobia@whirlpool
include $(INCLUDE_DIR)/package.mk

# +kmod-rt2800-usb

define Package/ext-rooter-basic
  SECTION:=utils
  CATEGORY:=ROOter
  SUBMENU:=Basic Support
  DEPENDS:=+luci-compat +kmod-usb-net +kmod-usb-net-huawei-cdc-ncm +kmod-usb-net-cdc-ether +kmod-usb-acm \
	    +kmod-usb-net-qmi-wwan  +kmod-usb-net-rndis +kmod-usb-serial-qualcomm \
	    +kmod-usb-net-sierrawireless +kmod-usb-ohci +kmod-usb-serial +kmod-nls-utf8 \
	    +kmod-usb-serial-option +kmod-usb-serial-sierrawireless +luci-proto-3x \
	    +kmod-usb-uhci +kmod-usb2 +luci-proto-3g +iptables-nft +ip6tables-nft \
	    +usb-modeswitch +wireless-tools +rmbim +rqmi +ext-sms +ext-buttons +kmod-rt2800-usb +xxd +kmod-tcp-bbr +kmod-usb3 
  TITLE:=ROOter support for usbmodems
  PKGARCH:=all
endef

define Package/ext-rooter-basic/description
  Helper scripts to enable ROOter to manage usb modem interfaces
endef


define Build/Compile
endef

define Package/ext-rooter-basic/install
	$(CP) ./files/* $(1)/


endef

$(eval $(call BuildPackage,ext-rooter-basic))
