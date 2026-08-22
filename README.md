# Ascender Execution Environment

[![CI](https://github.com/ctrliq/ascender-ee/actions/workflows/ci.yml/badge.svg)](https://github.com/ctrliq/ascender-ee/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/license-Apache--2.0-blue.svg)](./LICENSE.md)
[![Base](https://img.shields.io/badge/base-Rocky%20Linux%209-blue.svg)](https://rockylinux.org)

The default execution environment for [Ascender](https://github.com/ctrliq/ascender). It is the container image Ascender runs every job inside, built on Rocky Linux 9 with Python 3.12, `ansible-core`, `ansible-runner`, and a curated set of collections for the platforms customers automate most.

## Requirements

- [ansible-builder](https://ansible-builder.readthedocs.io/en/stable/installation/)
- Podman, or Docker with `--container-runtime=docker`

## Installation

Pull the published image rather than building it, unless you are changing its contents:

```bash
podman pull ghcr.io/ctrliq/ascender-ee:latest
```

## Using the execution environment

Run from the root of this repository:

```bash
ansible-builder build -v3 -t ghcr.io/ctrliq/ascender-ee
```

Add the image in Ascender under Administration then Execution Environments, then select it on a job template.

## Configuration

Image contents are declared in [`execution-environment.yml`](./execution-environment.yml):

| Key | Purpose |
| --- | ------- |
| `dependencies.galaxy` | Collections baked into the image, with pinned versions |
| `dependencies.python` | Python packages installed into the final image |
| `dependencies.system` | RPM packages, with `[platform:rpm]` build markers |
| `additional_build_steps` | Post-build patches, symlinks, and the `ascender` user |

## Included content

- **Base**: Rocky Linux 9 with Python 3.12 and `dnf` as the package manager
- **Ansible**: `ansible-core` 2.16, held below 2.17 to keep EL8 Python 3.6 support
- **Runtime**: `ansible-runner`, plus `receptor` for Ascender automation mesh
- **18 collections**, including `ctrliq.ascender`, AWS, Azure, GCP, VMware, and Windows
- **Credential support**: Kerberos, CredSSP, WinRM, PSRP, and `ansible-sign`

## Testing

CI builds the image on every pull request, which is the check that matters here.

- **Build**: `ansible-builder build -v3 -t ghcr.io/ctrliq/ascender-ee`
- **Lint**: `tox`

## The Ascender ecosystem

| Repository | Description |
| ---------- | ----------- |
| [ascender](https://github.com/ctrliq/ascender) | The platform itself: web UI, REST API, and task engine |
| [ascender-install](https://github.com/ctrliq/ascender-install) | Installer for Ascender and Ledger, with Galaxy Proxy support |
| [ascender-k8s-install](https://github.com/ctrliq/ascender-k8s-install) | Kubernetes installer for Ascender, Ledger, and React |
| [ascender-pro-install](https://github.com/ctrliq/ascender-pro-install) | Enhanced installer adding Reaqt, Registry, and Galaxy Proxy |
| [ascender-operator](https://github.com/ctrliq/ascender-operator) | Kubernetes operator that deploys and manages Ascender |
| [ascender-ee](https://github.com/ctrliq/ascender-ee) | Default execution environment image for Ascender jobs |
| [ascender-kit](https://github.com/ctrliq/ascender-kit) | The `ascender` command line client and Python API library |
| [ascender-collection](https://github.com/ctrliq/ascender-collection) | The `ctrliq.ascender` Ansible collection for a controller |
| [ascender-ledger](https://github.com/ctrliq/ascender-ledger) | Reporting tool for host facts and playbook changes |
| [ascender-galaxy-proxy](https://github.com/ctrliq/ascender-galaxy-proxy) | Caching proxy for Ansible Galaxy collection downloads |
| [ascender-playbooks](https://github.com/ctrliq/ascender-playbooks) | Example playbooks for use with Ascender |
## Contributing

- See [CONTRIBUTING.md](./CONTRIBUTING.md) for development setup, testing, and pull requests.
- Report bugs and collection requests via [GitHub Issues](https://github.com/ctrliq/ascender-ee/issues).
- For security vulnerabilities, follow [SECURITY.md](./SECURITY.md) rather than opening an issue.
- Join the [Ascender forum](https://forum.ascender-automation.org) to discuss development topics.

## License

Licensed under the **Apache License 2.0**. See [LICENSE.md](./LICENSE.md) for the full text.
