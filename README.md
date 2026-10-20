# biglinux-transitional-packages

Empty **transitional packages** for packages retired from the BigLinux
repositories.

A package that simply disappears from the repository stays installed forever
on systems that are never reinstalled. Publishing an empty package with a
newer version fixes that: on the next upgrade pacman installs the empty
version, which removes the old files, and pulls in the replacement when there
is one (`depends`). After that the empty package can be removed.

| Package | Why it was retired | Replacement |
|---|---|---|
| `stadia-controller-udev` | Google Stadia ended in January 2023; the rules gave world-writable access to every HID device of whole vendors | — |
| `openrgb-udev-rules` | Manjaro's `openrgb` ships the same `60-openrgb.rules` | `openrgb` |

## Retiring another package

1. Add its name to `pkgname` in `pkgbuild/PKGBUILD`.
2. Add a `package_<name>()` function with a `pkgdesc` saying why, and
   `depends=('<replacement>')` if something took its place.
3. Remove the package from the ISO lists (`iso-profiles`) and build this
   repository for the **stable** repository with gitrepo.

The packages go to `stable`, not `extra`: the AUR automation watches `extra`
and would rebuild the old package from the AUR.

## License

GPL-3.0-or-later. See [LICENSE](LICENSE).
