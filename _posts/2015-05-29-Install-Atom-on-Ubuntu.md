---
layout:     post
title:      Install Atom Editor on Ubuntu
date:       2015-05-29 23:00:00
summary:    Installing Atom editor on Ubuntu or Linux Mint
categories: atom ubuntu linux-mint
---

Installing or updating Atom editor on Ubuntu or Linux Mint is not possible
through apt-get but is quite easy.

First, download the package using `wget`:

```bash
$ wget https://atom.io/download/deb
```

When the download is finished, install the package using `dpkg`:

```bash
$ sudo dpkg --install atom-amd64.deb
```

Finally launch atom editor:

```bash
$ atom
```

and you have it.

![Atom screenshot]({{ site.url }}/assets/Screenshot-2015-05-29.png)
