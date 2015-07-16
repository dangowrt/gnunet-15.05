## GNUnet package feed

for OpenWrt 15.05 Chaos Calmer


### Usage

Download the OpenWrt SDK e.g. `OpenWrt-SDK-15.05-rc3-ar71xx-generic_gcc-4.8-linaro_uClibc-0.9.33.2.Linux-x86_64.tar.bz2`
depending on your target platform. Unpack it, cd into the created directory. 
There run
```shell
cp feeds.conf.default feeds.conf
```

Make sure feeds.conf also contains a git-src for the base packages, if not
```shell
echo "src-git base git://git.openwrt.org/15.05/openwrt.git" > feeds.conf
cat feeds.conf.default >> feeds.conf
```

Add the gnunet package feed
```shell
echo "src-git gnunet https://github.com/dangowrt/gnunet-15.05.git" >> feeds.conf
```

Some packages are already provided by OpenWrt's packages.git,
but in an older version. Make sure to install the recent versions
by running
```shell
scripts/feeds update -a
scripts/feeds uninstall -a
scripts/feeds install -a -p gnunet
```

Now run `make` to build all packages from this feed (and all packages
they depend on, so this may take a while...)
