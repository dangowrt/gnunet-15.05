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
echo "src-git gnunet https://github.com/dangowrt/gnunet-15.05.git" > feeds.conf
cat feeds.conf.default >> feeds.conf
```

If you are using a pre-built SDK, make sure feeds.conf also contains a
git-src for the base packages, if not
```shell
echo "src-git base git://git.openwrt.org/15.05/openwrt.git" >> feeds.conf
```

Also make sure the right branch `for-15.05` is used for all feeds and
comment-out the targets feed which doesn't provide anything for CC.
The final `feeds.conf` should look like this

```
src-git gnunet https://github.com/dangowrt/gnunet-15.05.git
src-git packages https://github.com/openwrt/packages.git;for-15.05
src-git luci https://github.com/openwrt/luci.git;for-15.05
src-git routing https://github.com/openwrt-routing/packages.git;for-15.05
src-git telephony https://github.com/openwrt/telephony.git;for-15.05
src-git management https://github.com/openwrt-management/packages.git;for-15.05
#src-git targets https://github.com/openwrt/targets.git;for-15.05
src-git base git://git.openwrt.org/15.05/openwrt.git
```

Some packages are already provided by OpenWrt's packages.git, but in an older
version. Make sure to prefer the recent versions from this feed by running
```shell
scripts/feeds update -a
scripts/feeds uninstall -a
scripts/feeds install -a -p gnunet
```

When using a pre-built SDK, avoid build problems by uninstalling some superflus
packages
```shell
scripts/feeds uninstall libgdbm python
```

When building from source use `make menuconfig` and choose the target platform
as well as the packages you want.

Now run `make` to build them (and all packages they depend on, so this may take
a while...)
