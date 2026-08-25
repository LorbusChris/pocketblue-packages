# COPR always invokes THIS file (make -f <repo>/.copr/Makefile srpm) with the
# package's subdirectory as CWD. Packages that need more than spec+sources in
# their directory -- e.g. surface/libwacom, which pulls Fedora's spec at
# build time -- carry their own .copr/Makefile and are delegated to; every
# other package gets the classic flow below.
srpm:
	@if [ -f .copr/Makefile ]; then \
		make -f .copr/Makefile srpm outdir="$(outdir)"; \
	else \
		sed -i -e "s/%autorelease/$$(date +%s)%{?dist}/" *.spec && \
		dnf install -y rpkg rpmdevtools && \
		spectool -g *.spec && \
		rpkg srpm --outdir=. && \
		mv *.src.rpm $(outdir)/; \
	fi
