# Maintainer: SquidRings <squidrings4@gmail.com>

pkgname=foxos-openbox
pkgver=2.0
pkgrel=0
pkgdesc="Openbox WM Configurations for foxos"
url="https://github.com/Foxos-package/foxos-openbox"
arch=('any')
license=('GPL3')
makedepends=()
depends=('openbox' 'obconf'
		'obmenu-generator' 'perl-linux-desktopfiles'
		'xfce4-settings' 'xfce4-power-manager' 'xfce4-terminal'
		'nitrogen' 'alacritty' 'thunar' 'geany'
		'rofi' 'polybar' 'dunst'
		'mpd' 'mpc' 'ffmpeg'
		'maim' 'xclip' 'viewnior'
		'ksuperkey' 
		'betterlockscreen'
		'networkmanager-dmenu-git'
		'xorg-xsetroot'
		'xmlstarlet'
		'yad'
		'python2'
)
conflicts=()
provides=("${pkgname}")
options=(!strip !emptydirs)
install="${pkgname}.install"

prepare() {
	cp -af ../files/. ${srcdir}
}

package() {
	local _sharedir=${pkgdir}/usr/share/foxos/openbox
	local _obdir=${pkgdir}/etc/skel/.config/openbox
	local _configdir=${pkgdir}/etc/skel/.config

	mkdir -p "$_sharedir" && mkdir -p "$_obdir" && mkdir -p "$_configdir"

	# Copy shared files & fix permissions
	cp -r ${srcdir}/icons 				"$_sharedir"
	cp -r ${srcdir}/menulib 			"$_sharedir"
	cp -r ${srcdir}/pipemenus 			"$_sharedir"
	chmod +x "$_sharedir"/pipemenus/*
	
	# Copy openbox specific configs
	cp -r ${srcdir}/alacritty 				"$_configdir"
	cp -r ${srcdir}/dconf 					"$_configdir"
	cp -r ${srcdir}/dunst 					"$_configdir"
	cp -r ${srcdir}/networkmanager-dmenu 	"$_configdir"
	cp -r ${srcdir}/nitrogen 				"$_configdir"
	cp -r ${srcdir}/obmenu-generator 		"$_configdir"
	cp -r ${srcdir}/plank 					"$_configdir"
	cp -r ${srcdir}/Thunar 					"$_configdir"
	cp -r ${srcdir}/xfce4 					"$_configdir"
	install -Dm 644 picom.conf				"$_configdir"/picom.conf

	# Copy window manager configs
	cp -r ${srcdir}/polybar 			"$_obdir"
	cp -r ${srcdir}/rofi 				"$_obdir"
	cp -r ${srcdir}/scripts 			"$_obdir"
	chmod +x "$_obdir"/scripts/*
	chmod +x "$_obdir"/rofi/bin/*
	
	launch_files=(`find ${_obdir}/polybar -type f | grep launch.sh`)
	for _file in "${launch_files[@]}"; do
		chmod +x ${_file}
	done

	scripts_dir=(`find ${_obdir}/polybar -type d | grep scripts`)
	for _script in "${scripts_dir[@]}"; do
		chmod +x ${_script}/*
	done

	install -Dm 755 autostart   		"$_obdir"/autostart
	install -Dm 644 rc.xml				"$_obdir"/rc.xml
	install -Dm 644 menu-glyphs.xml		"$_obdir"/menu-glyphs.xml
	install -Dm 644 menu-icons.xml		"$_obdir"/menu-icons.xml
	install -Dm 644 menu-minimal.xml	"$_obdir"/menu-minimal.xml
	install -Dm 644 menu-simple.xml		"$_obdir"/menu-simple.xml
}
