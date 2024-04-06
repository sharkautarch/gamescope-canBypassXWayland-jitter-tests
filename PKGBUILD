# Modified version of archlinux repo gamescope PKGBUILD file - sharkautarch
# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Giancarlo Razzolini <grazzolini@archlinux.org>
# Contributor: Samuel "scrufulufugus" Monson <smonson@irbash.net>
# Contributor: PedroHLC <root@pedrohlc.com>

pkgname=gamescope
pkgver=3.14.21
pkgrel=1
pkgdesc='SteamOS session compositing window manager'
arch=(x86_64)
url=https://github.com/ValveSoftware/gamescope
license=(BSD)
depends=(
  gcc-libs
  glibc
  glm
  libavif
  libcap.so
  libdisplay-info.so
  libdrm
  libliftoff.so
  libpipewire-0.3.so
  libvulkan.so
  libx11
  libxcb
  libxcomposite
  libxdamage
  libxext
  libxfixes
  libxkbcommon.so
  libxmu
  libxrender
  libxres
  libxtst
  libxxf86vm
  openvr
  sdl2
  vulkan-icd-loader
  wayland
  xorg-server-xwayland
)
makedepends=(
  benchmark
  git
  glslang
  meson
  ninja
  vulkan-headers
  wayland-protocols
)
#_tag=bca7990e61a1eb8198e54d86a4a9a44d41d9b07e
source=(
  git+https://github.com/sharkautarch/gamescope.git
  #git+https://github.com/ValveSoftware/gamescope.git
  git+https://github.com/Joshua-Ashton/reshade.git
  git+https://github.com/KhronosGroup/SPIRV-Headers.git
)
b2sums=('SKIP'
        'SKIP'
        'SKIP')
options=(!strip)
prepare() {
  cd gamescope
  #git checkout gs_wsi_xcb_optimization-v2
  #git checkout test_canBypassWayland_duration
  #git checkout test_w_no_lut
  #git checkout gs_wsi_xcb_optimization-v2-test-duration
  git checkout test_canBypassWayland-v2_duration
  #git checkout test_w_no_lut_newer
  git submodule update --init
  #git checkout test
  #git checkout master
  #git checkout gs-dispatch-descriptor-changes
  #git checkout fix-possible-crash-due-to-race
  #git checkout layer-maintenance1-framelatencyaware
  meson subprojects download
  #git submodule update --init subprojects/vkroots
  #git submodule init src/reshade
  #git config submodule.src/reshade.url ../reshade
  #git submodule init thirdparty/SPIRV-Headers
  #git config submodule.thirdparty/SPIRV-Headers.url ../SPIRV-Headers
  #git -c protocol.file.allow=always submodule update
  
  #cd subprojects/vkroots
  #echo 'git remote add sharkautarch https://github.com/sharkautarch/vkroots.git'
  #if [ -z $(git remote | grep sharkautarch) ]; then
  #	git remote add sharkautarch https://github.com/sharkautarch/vkroots.git
  #fi
  #echo ''
  #echo 'git config pull.rebase false'
  #git config pull.rebase false
  #echo ''
  #echo "PWD=$(pwd)"
  #echo ''
  #echo 'git fetch sharkautarch'
  #echo ''
  #git fetch sharkautarch
  #git pull sharkautarch  fix_deadlock_match_gamescope_ver
  #git checkout main
  #git pull
  #git checkout sync-fixes-edited
  #gen/make_vkroots
  #cd ../..
  
}

#pkgver() {
#  cd gamescope
#  git describe --tags | sed 's/-//' | tr '-' ' ' | awk '{print $1}'
#}

build() {
  LDFLAGS=""
  CXXFLAGS=""
  #cd $srcdir/$pkgname
  #cd $srcdir
  #--compress-debug-sections=zstd
  CC=gcc CXX=g++ arch-meson --wipe --reconfigure --buildtype=release -Dc_args="-g1 -Wno-error=unused-but-set-variable -Wno-error=unused-variable -fipa-pta -fdelete-dead-exceptions -march=native -Wno-error=stringop-overflow -fno-omit-frame-pointer" -Dc_link_args="-g1 -Wno-error=unused-but-set-variable -Wno-error=unused-variable -fdelete-dead-exceptions -fipa-pta -march=native -Wl,--strip-discarded,--gc-sections,--relax,-z,start-stop-gc,-z,pack-relative-relocs,-O1 -Wno-error=stringop-overflow -fno-omit-frame-pointer" -Dcpp_args="-g1 -fnothrow-opt -fno-threadsafe-statics -fimplicit-constexpr -fno-enforce-eh-specs -fno-check-new -Wno-error=unused-but-set-variable -Wno-error=unused-variable -fdelete-dead-exceptions -fipa-pta -march=native -fno-omit-frame-pointer" -Dcpp_link_args="-g1 -fno-threadsafe-statics -fimplicit-constexpr -fnothrow-opt -fno-check-new -fno-enforce-eh-specs -Wno-error=unused-but-set-variable -Wno-error=unused-variable -fdelete-dead-exceptions -march=native -fipa-pta -Wl,--strip-discarded,--gc-sections,--relax,-z,start-stop-gc,-z,pack-relative-relocs,-O1 -fno-omit-frame-pointer" -Db_lto=true -Db_ndebug=true -Db_sanitize=none -Denable_openvr_support=false gamescope build \
    -Dforce_fallback_for=stb,wlroots,vkroots,wayland \
    -Dpipewire=enabled
  CC=gcc CXX=g++ meson compile -C build
}

package() {
  CC=gcc CXX=g++ DESTDIR="${pkgdir}" meson install -C build
  install -Dm 644 gamescope/LICENSE -t "${pkgdir}"/usr/share/licenses/gamescope/
}

# vim: ts=2 sw=2 et:
