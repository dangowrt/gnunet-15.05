## GNUnet-15.05 package feed

back-ported [GNUnet](https://www.gnunet.org/) packages for [OpenWrt](https://www.openwrt.org/) 15.05 Chaos Calmer

### Usage

Download the OpenWrt Chaos Calmer SDK, either use the pre-built SDK to create
packages usable on devices running binaries from OpenWrt.org ie. download and
unpack `OpenWrt-SDK-15.05-*.tar.bz2` for the OpenWrt target you want from
https://downloads.openwrt.org/chaos_calmer/

Alternatively, to build the whole firmware from source:
```shell
git clone git://git.openwrt.org/15.05/openwrt.git openwrt-15.05
```

Once cloned or unpacked, `cd` into the created directory.
There run
```shell
cp feeds.conf.default feeds.conf
```

If you are using a pre-built SDK, make sure feeds.conf also contains a
git-src for the base packages, if not
```shell
echo "src-git base git://git.openwrt.org/15.05/openwrt.git" > feeds.conf
cat feeds.conf.default >> feeds.conf
```

Then add the gnunet package feed
```shell
echo "src-git gnunet https://github.com/dangowrt/gnunet-15.05.git" >> feeds.conf
```

Some packages are already provided by OpenWrt's packages.git, but in an older
version. Make sure to prefer the recent versions from this feed by running
```shell
scripts/feeds update -a
scripts/feeds uninstall -a
scripts/feeds install -a -p gnunet
```

Use `make menuconfig` and choose the packages you want.
Now run `make` to build them (and all packages they depend on, so this may take
a while...)
