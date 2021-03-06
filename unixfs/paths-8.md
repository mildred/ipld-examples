# IPLD Pathing: (8) different delimiters, strict and explicit `link/`

These examples are IPLD pathing of the unixfs datastructure, in the "(8) different delimiters, strict and explicit `link/`" style.

Here we use:
- `/` to delimit object-local properties (could be `.`)
- `//` to delimit link-object resolution (could be `/`)

```
> ipld cat /ipfs/Qm-unixfs-dir0/foo1
---
link: /ipfs/Qm-unixfs-dir1
mode: 0777
size: 220

> ipld cat /ipfs/Qm-unixfs-dir0/foo1/link
"/ipfs/Qm-unixfs-dir1"
>
> ipld cat /ipfs/Qm-unixfs-dir0/foo1/link/
---
bar1:
  link: /ipfs/Qm-unixfs-dir3
  mode: 0777
  size: 120
bar2:
  link: /ipfs/Qm-unixfs-dir2 # note, same as foo2 above
  mode: 0777
  size: 140
>
> ipld cat /ipfs/Qm-unixfs-dir0/foo1/link/bar1/mode
0777
>
> ipld cat /ipfs/Qm-unixfs-dir0/foo1/link/bar1/size
120
>
> ipld cat /ipfs/Qm-unixfs-dir0/foo1/link/bar2/link/baz2/link/
> ipld cat /ipfs/Qm-unixfs-dir0/foo1//bar2//baz2//
---
body: "hello\n"

> ipld cat /ipfs/Qm-unixfs-dir0/foo1/link/bar2/link/baz2/link/body
> ipld cat /ipfs/Qm-unixfs-dir0/foo1//bar2//baz2//body
hello

>
> ipld cat /ipfs/Qm-unixfs-dir0/foo1/link/bar2/link/baz1/link/
> ipld cat /ipfs/Qm-unixfs-dir0/foo1//bar2//baz1//
---
files:
  - link: Qm-unixfs-file1
    size: 10
  - link: Qm-unixfs-file2
    size: 10
  - link: Qm-unixfs-file1
    size: 10
>
> ipld cat /ipfs/Qm-unixfs-dir0/foo1/link/bar2/link/baz1/link/body
> ipld cat /ipfs/Qm-unixfs-dir0/foo1//bar2//baz1//body
> # no body
```
