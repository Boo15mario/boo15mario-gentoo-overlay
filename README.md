# boo15mario-gentoo-overlay

This repository is a custom Gentoo overlay for System76 software, drivers, and follow-on packaging work such as a System76-focused kernel.

## Enable the overlay with `eselect repository`

Install the helper if it is not already present:

```bash
emerge --ask app-eselect/eselect-repository
```

Add the overlay with the git sync type:

```bash
eselect repository add boo15mario-gentoo-overlay git https://github.com/Boo15mario/boo15mario-gentoo-overlay.git
emaint sync -r boo15mario-gentoo-overlay
```

## Remove the overlay

```bash
eselect repository remove boo15mario-gentoo-overlay
```

## Overlay layout

This overlay now includes the minimal files Portage expects for a standalone overlay:

- `metadata/layout.conf`
- `profiles/repo_name`
- `profiles/categories`
- `system76/<package>/...`

The custom category is `system76`, so package directories live under `system76` first and then the package name.

## Initial System76 package namespace

The `system76` category is pre-created for the main System76 packages that are commonly documented together by System76 for non-Pop!_OS systems:

- `system76/firmware-manager`
- `system76/gnome-shell-extension-system76-power`
- `system76/launch`
- `system76/system76-acpi-dkms`
- `system76/system76-dkms`
- `system76/system76-driver`
- `system76/system76-firmware`
- `system76/system76-firmware-daemon`
- `system76/system76-io-dkms`
- `system76/system76-kernel`
- `system76/system76-power`
- `system76/system76-scheduler`

Each package directory includes `metadata.xml` so the package layout is ready for ebuilds to be added incrementally.

## System76 kernel plan

A `system76/system76-kernel` package directory is reserved for future kernel work. To make it behave more like `gentoo-kernel`, the next step would be to add an ebuild that:

1. pulls a known kernel source base,
2. applies a maintained System76 patch set from the package `files/` directory, and
3. reuses the standard Gentoo kernel workflow instead of inventing a separate install path.

That keeps the overlay aligned with normal Gentoo kernel maintenance while still leaving room for System76-specific patches.
