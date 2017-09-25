---
title: "Mount Android in Linux"
header:
  image: /assets/images/unsplash-2.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
categories:
  - Linux
tags:
  - Android
---

To communicate with Android Phone in Linux, 
we have to use [MTP](https://en.wikipedia.org/wiki/Media_Transfer_Protocol), 
Media Transfer Protocol.

## Installation

Linux MTP support is provided by [libmtp](https://www.archlinux.org/packages/?name=libmtp) package.

For CLI, I recommend use AUR package [simple-mtpfs](https://aur.archlinux.org/packages/simple-mtpfs/).

For GUI, I recommend use [Thunar](https://www.archlinux.org/packages/?name=thunar) file manager, 
[gvfs](https://www.archlinux.org/packages/?name=gvfs) virtual filesystem implementation for GIO, 
[gvfs-mtp](https://www.archlinux.org/packages/?name=gvfs-mtp) MTP backend, 
[thunar-volman](https://www.archlinux.org/packages/?name=gvfs-mtp) Thunar volume manager.

## Usage of simple-mtpfs

List detected devices

```sh
$ simple-mtpfs -l
1: AsusFonepad 7 (FE375CXG)
```

Mount device 1 on ~/mnt

```sh
$ simple-mtpfs --device 1 ~/mnt
```

Unmount mountpoint ~/mnt

```sh
$ fusermount -u ~/mnt
```

## Configuration of Thunar

To let Thunar handle automatice mounting, one must launch Thunar in daemon mode.

So execute `thunar --daemon` as login, one may add this command into i3 config file for startup.

And launch Thunar and go to _Edit_ > _Preferences_, check _Enable Volume Managerment_ under the _Advanced_ tab.

![thunar-volman-1]({{ site.url }}{{ site.baseurl }}/assets/images/thunar-volman-1.png)

Check _Mount removable drivers when hot-plugged_, _Mount removable media wehn inserted_.

![thunar-volman-2]({{ site.url }}{{ site.baseurl }}/assets/images/thunar-volman-2.png)

{% include toc title="Outline" icon="file-text" %}


