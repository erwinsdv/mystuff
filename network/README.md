## Router

I use a Xiaomi AX3000T as my main router.

I got the router from
[AliExpress](https://nl.aliexpress.com/w/wholesale-xiaomi-ax3000t.html?spm=a2g0o.productlist.search.0)
for around 35 EUR.

Reviews indicated that OpenWrt works fine on this model, so I installed it using
the [official instructions](https://openwrt.org/inbox/toh/xiaomi/ax3000t). I
also replaced the stock Xiaomi bootloader with u-boot.

Every few months, I upgrade the router to the latest stable OpenWrt release. For
this model, the correct images can be found
[here](https://downloads.openwrt.org/releases/24.10.5/targets/mediatek/filogic/).
Replace `24.10.5` in the URL with the latest stable version when upgrading.

Since I’m using the u-boot setup, upgrades are done using the sysupgrade image,
with filenames along the lines of:
`xiaomi_mi-router-ax3000t-ubootmod-squashfs-sysupgrade.itb`

The upgrade is performed through the LuCI web interface by going to System →
Backup / Flash Firmware, selecting the Flash image, and starting the upgrade.

## Tailscale

I use Tailscale to connect my devices (PCs, laptop, etc.) to each other, which
gives me secure remote access between them.

Tailscale is installed on the router using a newer version than the default
OpenWrt package. I followed
[this guide](https://gunanovo.github.io/openwrt-tailscale/) to install it.

To manage Tailscale from the web interface, I use the
[LuCI Tailscale application](https://github.com/Tokisaki-Galaxy/luci-app-tailscale-community).
One nice thing about this LuCI app is the option to automatically configure the
firewall.

## Anything else

### Weekly Router Reboot via Cron

To keep the router stable, a weekly reboot is scheduled using `cron`.

#### Edit the Root Crontab

```bash
crontab -e
```

Add the following line to reboot every Monday at 06:00,

```bash
0 6 * * 1 /sbin/reboot
```

Enable if needed,

```bash
/etc/init.d/cron start
/etc/init.d/cron enable
/etc/init.d/cron status
```
