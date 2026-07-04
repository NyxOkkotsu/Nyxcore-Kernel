pkgbase=linux-nyxcore-infinity
pkgname=('linux-nyxcore-infinity' 'linux-nyxcore-infinity-headers')
pkgver=7.1.2
pkgrel=1
pkgdesc='Nyxcore custom kernel with Infinity scheduler'
arch=('x86_64')
url='https://github.com/galpt/infinity-scheduler'
license=('GPL-2.0-only')
makedepends=('bc' 'bison' 'cpio' 'flex' 'git' 'libelf' 'openssl' 'pahole' 'perl' 'python' 'rust' 'xz' 'zstd')
options=('!strip' '!debug')
source=(
  "linux-${pkgver}.tar.xz::https://cdn.kernel.org/pub/linux/kernel/v7.x/linux-${pkgver}.tar.xz"
  "infinity-scheduler::git+https://github.com/galpt/infinity-scheduler.git#branch=v3"
  'nyxcore.cfg'
  '99-nyxcore-infinity.conf'
)
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP')

prepare() {
  cd "linux-${pkgver}"

  if [[ -r /proc/config.gz ]]; then
    zcat /proc/config.gz > .config
  else
    make defconfig
  fi

  local patchdir="${srcdir}/infinity-scheduler/patches/stable/linux-7.1-infinity"
  local patchfile

  while IFS= read -r -d '' patchfile; do
    patch -Np1 -F 3 -i "$patchfile"
  done < <(find "$patchdir" -type f -name '*.patch' -print0 | sort -zV)

  scripts/kconfig/merge_config.sh -m .config "${srcdir}/nyxcore.cfg"
  make olddefconfig LOCALVERSION='-nyxcore-infinity'
}

build() {
  cd "linux-${pkgver}"
  make LOCALVERSION='-nyxcore-infinity' -j"$(nproc)" bzImage modules
}

package_linux-nyxcore-infinity() {
  cd "linux-${pkgver}"
  local kernelver
  kernelver="$(make -s LOCALVERSION='-nyxcore-infinity' kernelrelease)"
  make LOCALVERSION='-nyxcore-infinity' INSTALL_MOD_PATH="${pkgdir}/usr" modules_install
  install -Dm644 arch/x86/boot/bzImage "${pkgdir}/boot/vmlinuz-linux-nyxcore-infinity"
  install -Dm644 System.map "${pkgdir}/usr/lib/modules/${kernelver}/System.map"
  install -Dm644 .config "${pkgdir}/usr/lib/modules/${kernelver}/config"
  install -dm755 "${pkgdir}/usr/lib/modules/${kernelver}"
}

package_linux-nyxcore-infinity-headers() {
  cd "linux-${pkgver}"
  local kernelver
  kernelver="$(make -s LOCALVERSION='-nyxcore-infinity' kernelrelease)"
  install -dm755 "${pkgdir}/usr/lib/modules/${kernelver}/build"
  cp -a --no-preserve=ownership . "${pkgdir}/usr/lib/modules/${kernelver}/build"
  rm -f "${pkgdir}/usr/lib/modules/${kernelver}/build/arch/x86/boot/bzImage"
}