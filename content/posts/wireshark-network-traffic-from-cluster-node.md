---
title: "Wireshark - network traffic from cluster node"
date: 2020-02-14
publishdate: 2020-02-14
lastmod: 2020-02-14
draft: false
tags: ["wireshark", "linux", "windows", "plink"]
---

Because `tcpdump` can write raw packets to standard output (**-w -** option), and Wireshark can read from standard input (**-i -** option), we can use `ssh` or `plink.exe` and redirect `tcpdump` output on a remote machine to a local Wireshark. `plink.exe` is a command-line connection tool similar to UNIX ssh mostly used for automated operations.

## Linux example

```
wireshark -k -i < (ssh _NODE_ sudo tcpdump -nnqt -s 0 -i any -A "portrange 5060-5099 or proto gre" -U -w -)
```

## Windows example

```
"C:\Program Files\PuTTY\plink.exe" -batch -ssh _NODE_ sudo tcpdump --immediate-mode -nnqt -s 0 -i any "portrange 5060-5099 or proto gre" -U -w - | "C:\Program Files\Wireshark\Wireshark.exe" -k -i -
```

