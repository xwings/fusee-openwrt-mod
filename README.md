# Fusee-lede Quick Mod

Mod from: https://github.com/DavidBuchanan314

Instructions/files for building a custom LEDE/OpenWRT image to turn cheap routers into a Nintendo Switch "modchip"/"dongle"

These instructions target the "MT7682" devices, although you should be able to make this work on any router with USB host support.


# Usage

Once installed, just plug in your switch in RCM mode, and the payload will get launched automagically!

Note: payload.bin is from https://sx.xecuter.com/download/payload.bin

# Compiling From Source

1. Clone this repo, and the main LEDE / Openwrt repo

```sh
git clone https://github.com/xwings/fuse-openwrt-mod
git clone -b lede-17.01 https://git.openwrt.org/source.git fusee-openwrt-img
```

2. Copy over the `fusee-nano` package, and the EHCI patch

```sh
cp -r fusee-openwrt-mod/fusee-nano-mod fusee-openwrt-img/package/utils/
cp fusee-openwrt-mod/899-ehci_enable_large_ctl_xfers.patch fusee-openwrt-img/target/linux/generic/patches-4.4/
```

3. Update LEDE feeds and configure

```
cd fusee-openwrt-img
./scripts/feeds update -a
./scripts/feeds install -a

make menuconfig
```

If you run into issues here, refer to https://wiki.openwrt.org/doc/howto/build

When in the configuration menu, you will need to set the following options:

```
Target System               => MediaTek Ralink MIPS
Subtarget                   => MT7688 based boards
Target Profile              => Default
Utilities > fusee-nano-mod  => <*>
LuCI > Collections          => luci
LuCI > Applications         => luci-app-command

```

4. Compile!

```
make -j12
```
If all goes well, you should find files ready to flash here:

```
bin/targets/ramips/mt7688/lede-ramips-mt7688-widora-neo-squashfs-sysupgrade.bin
```
