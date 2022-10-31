# rhel9-nautilus-typeahead

Port of a patch to add typeahead navigation to nautilus for distributions based on RHEL 9.

Thanks to Ian Hernández and Albert Vaca Cintora for providing the patch for [Archlinux AUR](https://aur.archlinux.org/cgit/aur.git/?h=nautilus-typeahead).

For more information see [this issue](https://gitlab.gnome.org/GNOME/nautilus/-/issues/1157).

## Build and install

### Pre-built rpm
Grab the .rpm from the release page in this repository and install via dnf:

```
# dnf install /path/to/nautilus-<version>.patched.el9.<arch>.rpm /path/to/nautilus-extensions-<version>.patched.el9.<arch>.rpm
```

### Manually building from source code
Grab the nautilus .src.rpm from your distribution's repository. extract it to /home/$USER/rpmbuild/SOURCES/ and replace the nautilus.spec file from the one provided in this repository and put the patch next to other patches. Then run rpmbuild to create rpm package:

```
$ rpmbuild -bb /home/$USER/rpmbuild/SOURCES/nautilus.spec
```

Alternatively you can use the pre-patched .src.rpm provided in the release page and build it directly:

```
$ rpmbuild --rebuild /path/to/nautilus-<version>.patched.el9.src
```

once the build is completed you can install using dnf:

```
# dnf install /home/$USER/rpmbuild/RPMS/<arch>/nautilus-<version>.patched.el9.<arch>.rpm /home/$USER/rpmbuild/RPMS/<arch>/nautilus-extensions-<version>.patched.el9.<arch>.rpm
```

## Usage
After installation kill existing nautilus process by running `nautilus -q` and launch it again. Then simply start typing on your keyboard and the corresponding file will be highlighted as in any other file manager.

### known issues
- In wayland, the typeahead textbox opens in the middle of the window instead of bottom corner, this is because there is currently no way for a window to position itself in wayland session. 
- Nautilus crashes if you attempt to use typeahead navigation in `other-locations:///`
