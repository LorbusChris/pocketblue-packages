# libwacom with the linux-surface patches: virt/mei bus matching and the
# Microsoft Surface tablet definitions, which stock libwacom cannot express
# (it rejects the DeviceMatch entries and never maps BUS_VIRTUAL devices,
# so iptsd's pen devices stay unmatched).
#
# The spec is Fedora's own, pulled from rawhide at SRPM time so the
# packaging never drifts (every current branch ships libwacom 2.19.0); the
# release becomes a timestamp tagged .surface so this build version-wins
# over the stock package in any chroot, the same way the surface kernel
# does. The patch is the squashed linux-surface/libwacom ipts branch --
# regenerate it from there when it moves (provenance in the patch header).
srpm:
	dnf install -y rpkg rpmdevtools curl
	curl -sf -o libwacom.spec https://src.fedoraproject.org/rpms/libwacom/raw/rawhide/f/libwacom.spec
	sed -i -e "s/^Release:.*/Release: $(shell date +%s).surface%{?dist}/" libwacom.spec
	sed -i -e "/^Source0:/a Patch1000: 0001-surface-virt-mei-bus-and-tablets.patch" libwacom.spec
	spectool -g libwacom.spec
	rpkg srpm --outdir=.
	[ "$(outdir)" -ef . ] || mv *.src.rpm $(outdir)/
