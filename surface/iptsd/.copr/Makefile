# iptsd, from linux-surface's own repository: their iptsd.spec lives at the
# repo root and is rpkg-templated (Source: {{{ create_tarball }}} packs the
# checkout itself), so the build is a clone at the pinned tag plus rpkg run
# inside it -- the spec's home stays the one source of truth, same
# philosophy as surface/libwacom pulling Fedora's spec. The pin below is
# what Renovate bumps; the merged bump rebuilds the package through the
# path-filtered COPR webhook. Previously the COPR package cloned upstream
# directly with the tag pinned only in COPR's own config, where nothing
# could follow it.
#
# renovate: datasource=github-tags depName=linux-surface/iptsd
IPTSD_REF=v3.1.0

srpm:
	dnf install -y rpkg git
	git clone --depth 1 --branch $(IPTSD_REF) https://github.com/linux-surface/iptsd iptsd-src
	cd iptsd-src && rpkg srpm --outdir="$(outdir)"
