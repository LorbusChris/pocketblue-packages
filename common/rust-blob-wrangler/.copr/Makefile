# rust-blob-wrangler, from pocketblue's blob-wrangler fork: packit
# prepare-sources runs the upstream packaging job (the spec plus a `cargo
# package` crate archive built from the checked-out commit, so nothing
# depends on crates.io at build time) -- the same flow the old COPR
# custom-script build ran, but pinned to a commit here in the repo, where
# Renovate can follow the branch and a merged bump rebuilds the package
# through the path-filtered webhook.
#
# renovate: datasource=git-refs depName=https://github.com/pocketblue/blob-wrangler branch=pocketblue-fixes
BLOB_WRANGLER_COMMIT=798629543c85172a1a2b38d57342a8575ac7a490

srpm:
	dnf install -y packit cargo git rpm-build
	git config --global user.email "copr@COPR"
	git config --global user.name "COPR"
	packit -d prepare-sources --result-dir "$$PWD/prep" \
		--ref $(BLOB_WRANGLER_COMMIT) --job-config-index 1 \
		--no-create-symlinks https://github.com/pocketblue/blob-wrangler
	rpmbuild -bs prep/*.spec \
		--define "_sourcedir $$PWD/prep" --define "_srcrpmdir $(outdir)"
