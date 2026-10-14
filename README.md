# pkg-cbsp-boot-utilities

This repository contains the Debian packaging for
[`cbsp-boot-utilities`](https://github.com/qualcomm/cbsp-boot-utilities), the
upstream project that hosts Qualcomm utilities and apps related to boot
firmware -- most notably `qcom-capsule-tool`, a set of tools for generating
and signing UEFI capsule files used for firmware updates on Qualcomm Linux
platforms.

This is a **packaging repository**, not the source repository: it builds
Debian packages from the upstream source and does not contain application
source code itself. Source code, feature development, and bug fixes for the
tool belong upstream, at
[qualcomm/cbsp-boot-utilities](https://github.com/qualcomm/cbsp-boot-utilities).

## Package

| | |
| --- | --- |
| Source package | `qcom-capsule-tool` |
| Binary package | `python3-qcom-capsule-tool` |
| Upstream project | [qualcomm/cbsp-boot-utilities](https://github.com/qualcomm/cbsp-boot-utilities) |

See [`debian/control`](https://github.com/qualcomm-linux/pkg-cbsp-boot-utilities/blob/qcom/debian/latest/debian/control)
on the `qcom/debian/latest` branch for the full package description and
build dependencies.

## Branches

This repository follows the standard
[Qualcomm `pkg-*` repository layout](https://qualcomm-confluence.atlassian.net/wiki/spaces/LinuxCoreOS/pages/2879858691/pkg-+repository+specification):

- **qli-ci** (default branch): CI workflow definitions and repository
  boilerplate (this README, license, contributing guidelines). Contains no
  packaging content.
- **qcom/debian/latest**: The actively maintained Debian packaging branch
  (`debian/` directory: `control`, `rules`, `changelog`, `copyright`, etc.).
  It is an orphan branch -- the upstream source is not committed to it;
  `debian/watch` tracks the upstream `main` branch HEAD as a snapshot,
  imported with `gbp import-orig --uscan`. See `debian/README.Debian` on
  that branch for details.
- **debian/pr/\***: Transient branches auto-created by CI to validate pending
  packaging changes before merge.

## CI Workflows

The `qli-ci` branch includes the following workflows in
`.github/workflows/`:

- **pkg-build.yml**: Builds the Debian package via the reusable
  `pkg-build-reusable-workflow.yml` in
  [qli-ci](https://github.com/qualcomm-linux/qli-ci).
- **pkg-pr-hook.yml**: Runs on pull requests targeting `debian/*` or
  `qcom/**` branches (e.g. `qcom/debian/latest`).
- **pkg-promote.yml** / **pkg-promote-prebuilt.yml**: Promote the package's
  tracked upstream version to a new release.
- **pkg-release.yml**: Triggers a release of the package.
- **debusine-pr-check.yml** / **debusine-pr-hook.yml** /
  **debusine-release.yml**: Integration with
  [Debusine](https://debusine.qualcomm.com) for build validation and
  release.
- **stale-issues.yaml**: Closes stale issues and pull requests with no
  recent activity.

To build the package manually instead of via CI, go to the *Actions* tab,
select the *Build* workflow, and click *Run workflow* (or run `gbp
buildpackage` locally against the `qcom/debian/latest` branch after
importing the upstream source with `gbp import-orig --uscan`; see
`debian/README.Debian` on that branch).

## Installation Instructions

```sh
sudo apt install ./python3-qcom-capsule-tool_x_arm64.deb
```

Use `apt install ./<file>.deb` rather than `dpkg -i`: the package depends
on `python3-libfdt` and `python3-pyelftools`, and only `apt` resolves and
installs those dependencies automatically from the configured apt sources.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to submit packaging changes,
and [CODE-OF-CONDUCT.md](CODE-OF-CONDUCT.md) for community guidelines.

For issues with `qcom-capsule-tool` itself (bugs, feature requests), please
open an issue on the
[upstream repository](https://github.com/qualcomm/cbsp-boot-utilities/issues)
instead. Use this repository's issue tracker only for problems with the
Debian packaging.

## Security

See [SECURITY.md](SECURITY.md) for how to report a vulnerability.

## License

pkg-cbsp-boot-utilities is licensed under the
[BSD-3-Clause License](https://spdx.org/licenses/BSD-3-Clause.html). See
[LICENSE.txt](LICENSE.txt) for the full license text.
