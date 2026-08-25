# iio-sensor-proxy: Fedora's own spec with the mobility delta rebased onto
# it at every build -- this is not a fork, just an overlay: a pinned
# upstream snapshot (hadess master, where Fedora releases from), the
# sensor-error patch, and ssc-support enabled with the libssc dependencies
# (libssc comes from this COPR, present in the buildroot). The release is a
# timestamp tagged .mobility so the build version-wins over stock at equal
# versions.
#
# renovate: datasource=git-refs depName=https://gitlab.freedesktop.org/hadess/iio-sensor-proxy branch=master
IIO_COMMIT=0085ddf8ecb173a1c5fcf2344aa40e561125354f

srpm:
	dnf install -y rpkg rpmdevtools curl
	curl -sf -o iio-sensor-proxy.spec https://src.fedoraproject.org/rpms/iio-sensor-proxy/raw/rawhide/f/iio-sensor-proxy.spec
	sed -i \
		-e "1i %global commit $(IIO_COMMIT)" \
		-e "s/^Release:.*/Release: $(shell date +%s).mobility%{?dist}/" \
		-e "s|^Source0:.*|Source0: %{url}/-/archive/%{commit}/%{name}-%{commit}.tar.gz|" \
		-e "/^Source0:/a Patch0001: 0001-WIP-iio-sensor-proxy.c-Do-not-exit-based-on-sensor-e.patch\nBuildRequires: pkgconfig(libssc)\nRequires: libssc\nRequires: dbus" \
		-e "s/-Dssc-support=disabled/-Dssc-support=enabled/" \
		-e "s/%autosetup -S git_am/%autosetup -S git_am -n %{name}-%{commit}/" \
		iio-sensor-proxy.spec
	spectool -g iio-sensor-proxy.spec
	rpkg srpm --outdir=.
	[ "$(outdir)" -ef . ] || mv *.src.rpm $(outdir)/
