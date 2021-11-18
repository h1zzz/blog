---
layout: post
title:  "OpenSSL common commands"
date:   2021-11-18 14:09:00 +0800
categories: notes
tags: openssl
---

## Use with compression

```bash
# compression
$ tar zcf - {infile} | openssl des3 -salt -k {password} -out {outfile}
# decompression
$ openssl des3 -d -k {password} -salt -in {infile} | tar xzf -
```

## Create a certificate

```bash
$ openssl genrsa -out {key.pem} 2048
$ openssl req -new -x509 -days 3650 -key {key.pem} -out {cert.pem} -subj "/C=US/ST= /L= /O= /OU= /CN= /emailAddress= "
```

## Randomly generate string

```bash
$ openssl rand [-base64 | -hex] [-out file] num
```

## SSL client and server

```bash
# server
$ openssl s_server -tls1_2 -cert {cert.pem} -key {key.pem} -accept {port}
```

```bash
# client
$ openssl s_client -tls1 -connect {host}:{port}
```
