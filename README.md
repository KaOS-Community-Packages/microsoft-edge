PKGBUILD file requires to run with ***--skipinteg*** option:
**-$ makepkg PKGBUILD --skipinteg**

The reason is due to an extraction of external files -- **Microsoft-Standard-Application-License-Terms--Standalone-(free)-Use-Terms.pdf** + **microsoft-edge-stable.sh** not included in the provided .DEB package.
The source for these files is in the Arch git repository: *https://aur.archlinux.org/cgit/aur.git/snapshot/microsoft-edge-stable-bin.tar.gz* which provides different SHA-256 checkSUM from being uploaded to GitHub.

Thanks for understanding.
Martin
