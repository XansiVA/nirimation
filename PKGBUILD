# Maintainer: XansiDev <chaoscatsofficial@gmail.com>
pkgname=nirimation
pkgver=1.0.0
pkgrel=1
pkgdesc="Animations for the Niri Wayland compositor"
arch=("any")
url="https://github.com/XansiVA/nirimation"
license=("MIT")
depends=("python>=3.11" "niri")
source=("$pkgname::git+${url}.git")
sha256sums=("SKIP")

package() {
    cd "$srcdir/$pkgname/animations"

    # Install the script to /usr/bin
    install -Dm755 nirimation "$pkgdir/usr/bin/nirimation"

    # Install KDL animation files to /usr/share/nirimation/
    install -dm755 "$pkgdir/usr/share/nirimation"
    for kdl in *.kdl; do
        [ -f "$kdl" ] || continue
        install -Dm644 "$kdl" "$pkgdir/usr/share/nirimation/$kdl"
    done

    # Install license if present (from repo root)
    if [ -f "$srcdir/$pkgname/LICENSE" ]; then
        install -Dm644 "$srcdir/$pkgname/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    fi
}

post_install() {
    echo ""
    echo "==> nirimation installed."
    echo "    KDL files are in /usr/share/nirimation/"
    echo "    Your user config lives at ~/.config/nirimation/config.toml"
    echo ""
    echo "    First run:"
    echo "      nirimation apply <name>"
    echo ""
    echo "    This will:"
    echo "      - Copy the animation to ~/.config/niri/nirimation.kdl"
    echo "      - Add a one-time include line to your niri config.kdl"
    echo "      - Reload niri"
    echo ""
    echo "    Run 'nirimation list' to see available animations."
    echo ""
}

post_remove() {
    echo ""
    echo "==> nirimation removed."
    echo "    The following were NOT automatically deleted:"
    echo "      ~/.config/nirimation/"
    echo "      ~/.config/niri/nirimation.kdl"
    echo ""
    echo "    Remove them manually if you want:"
    echo "      rm -rf ~/.config/nirimation"
    echo "      rm -f ~/.config/niri/nirimation.kdl"
    echo ""
    echo "    Also remove the include line from ~/.config/niri/config.kdl if present."
    echo ""
}
