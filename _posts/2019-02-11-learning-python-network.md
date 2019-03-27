---
layout: post
title: "Learning Python: Network"
date: 2019-02-11 15:00:00 +0100
category: tutorial
tagline: ""
tags: [Python]
abstract : "Learning Note: network programming such as http, ftp, pop3, IRC."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Sockets via TCP and UDP](#sockets-via-tcp-and-udp)
    - [socket Module](#socket-module)
    - [socketserver Module](#socketserver-module)
* [FTP](#ftp)
* [Email Protocols](#email-protocols)
    - [poplib Module](#poplib-module)
    - [imaplib Module](#imaplib-module)
    - [smtplib Module](#smtplib-module)
    - [smtpd Module](#smtpd-module)
* [Other Application Protocols](#other-application-protocols)
    - [Telnet](#telnet)
    - [NNTP](#nntp)
    - [IRC](#irc)
* [References](#references)


## Introduction

I will introduce some modules about network programming for Internet protocols such as TCP, UDP, HTTP, FTP, POP3 and some other application layer protocols.
Mostly, the applications developed with these modules are clients.

> The examples below mainly use Python 3.x. The modules and codes are a little different in Python 2.x.


## Sockets via TCP and UDP

Sockets are widely used.
Python provides two modules, [socket](https://docs.python.org/3/library/socket.html){:target="_blank"} and [socketserver](https://docs.python.org/3/library/socketserver.html){:target="_blank"}, to communicate via socket interface.
The former provides access to the BSD socket interface.; the latter simplifies the task of writing network servers.

### _socket_ Module

This module provides several functions, constants and exceptions. Some functions can be used to create socket objects to deal with network-related services.

Here are applications about connection via sockets using TCP/IP protocol (IPv4): a server that listens to a port; and a client connects to it and sends message to it.

An example for server side:
```python
#!/usr/bin/env python3

import socket

HOST = ""           # Symbolic name meaning all available interfaces
PORT = 40480

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((HOST, PORT))
    s.listen(1)
    conn, addr = s.accept()
    with conn:
        print("Connected by", addr)
        while True:
            data = conn.recv(1024)
            if not data:
                break
            print("Received:", data.decode())
            conn.sendall(("Reply to:"+data.decode()).encode())
```

An example for client side:
```python
#!/usr/bin/env python3

import socket

HOST = "localhost"
PORT = 40480

with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    s.sendall(b"Hello, zhuzhu!")
    data = s.recv(1024)
    print("Received:", data.decode())
```

### _socketserver_ Module

This module is used to create network servers simply.
There are four basic concrete server classes: TCPServer, UDPServer, UnixStreamServer and UnixDatagramServer.

An example for a TCP server:
```python
#!/usr/bin/env python3.5

import socketserver

class ZhuTCPHandler(socketserver.BaseRequestHandler):

    def handle(self):
        self.data = self.request.recv(1024).decode().strip()
        print("{0} sent:\n{1}".format(self.client_address[0], self.data))
        self.request.sendall(("Reply: " + self.data).encode())

if __name__ == "__main__":
    HOST, PORT = "localhost", 40480
    s = socketserver.TCPServer((HOST, PORT), ZhuTCPHandler)
    s.serve_forever()
```

An example for a UDP server:
```python
#!/usr/bin/env python3

import socketserver

class ZhuUDPHandler(socketserver.BaseRequestHandler):

    def handle(self):
        self.data = self.request[0].decode().strip()
        self.socket = self.request[1]
        print("{0} sent:\n{1}".format(self.client_address[0], self.data))
        self.socket.sendto(("Reply: " + self.data).encode(), self.client_address)

if __name__ == "__main__":
    HOST, PORT = "localhost", 40480
    s = socketserver.UDPServer((HOST, PORT), ZhuUDPHandler)
    s.serve_forever()
```

The client for UDP uses a different type of packet:
```python
#!/usr/bin/env python3

import socket
import sys

HOST, PORT = "localhost", 40480
data = "Hello, zhuzhu!"

sock = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

sock.sendto(data.encode(), (HOST, PORT))
received = sock.recv(1024).decode()

print("Received: {0}".format(received))
```


## FTP

The [ftplib](https://docs.python.org/3/library/ftplib.html){:target="_blank"} module defines the class `FTP` and a few related items.
We could use it to implement the client side of the FTP (File Transfer Protocol) protocol:
1. connecting to an FTP server;
2. listing directory and accessing remote files;
3. downloading files;
4. uploading files.

```python
#!/usr/bin/env python3

from ftplib import FTP

ftp = FTP("mirror.reverse.net")
ftp.login("anonymous", "anonymous")
ftp.dir()
ftp.cwd("pub/apache/opennlp/models/langdetect/1.8.3")
ftp.retrlines("LIST")
ftp.retrbinary("RETR README.txt", open("README.local", "wb").write)
ftp.quit()
```

With another class `FTP_TLS`, we could implement TLS support.


## Email Protocols

Email Protocols include _POP3 (Post Office Protocol 3)_, _IMAP (Internet Message Access Protocol)_ and _SMTP (Simple Mail Transfer Protocol)_.
Python provides corresponded modules, `poplib`, `imaplib`, `smtplib` and `smtpd`, to develop email-related applications.
Besides, the modules `email`, `mailbox` and `mimetypes` can help to manage email messages.

### _poplib_ Module

The [poplib](https://docs.python.org/3.5/library/poplib.html){:target="_blank"} module defines a class, `POP3`, which encapsulates a connection to a POP3 server and implements the protocol as defined in [RFC 1939](https://tools.ietf.org/html/rfc1939.html){:target="_blank"}.

It supports both standard POP3 (it could also start a TLS session) or POP3 with SSL connection.

```python
#!/usr/bin/env python3

import getpass, poplib

# connect to the server using POP3 over an SSL encrypted socket.
M = poplib.POP3_SSL(host="pop.gmail.com", port=995)
# login with username and password
M.user(getpass.getuser())
M.pass_(getpass.getpass())

numMessages = len(M.list()[1])
for i in range(numMessages):
    for j in M.retr(i+1)[1]:
        print(j)

M.quit()
```

### _imaplib_ Module

The [imaplib](https://docs.python.org/3.5/library/imaplib.html){:target="_blank"} module defines three classes, `IMAP4`, `IMAP4_SSL` and `IMAP4_stream`, which encapsulate a connection to an IMAP4 server and implement a large subset of the IMAP4rev1 client protocol. It is backward compatible with IMAP4 servers.

```python
#!/usr/bin/env python3

import getpass, imaplib

M = imaplib.IMAP4_SSL(host="imap.gmail.com", port=993)
M.login(getpass.getuser(), getpass.getpass())
M.select()

typ, data = M.search(None, "ALL")
for num in data[0].split():
    typ, data = M.fetch(num, "(RFC822)")
    print('Message %s\n%s\n' % (num, data[0][1]))

M.close()
M.logout()
```

### _smtplib_ Module

The [smtplib](https://docs.python.org/3.5/library/smtplib.html){:target="_blank"} module defines an SMTP client session object that can be used to send mail to any Internet machine with an SMTP or ESMTP listener daemon.

It offers three classes, `SMTP`, `SMTP_SSL` and `LMTP`, to encapsulate an SMTP or ESMTP connection.

```python
#!/usr/bin/env python3

import smtplib

fromaddr = "from@zhuzhu.org"
toaddrs = ["to@zhuzhu.org"]
msg = ("From: %s\r\nTo: %s\r\n\r\n" % (fromaddr, ", ".join(toaddrs))) + "This is a test email."

server = smtplib.SMTP(host="localhost", port=40480)
server.set_debuglevel(1)
server.sendmail(fromaddr, toaddrs, msg)
server.quit()
```

We can use the `email` package to read, write simple email messages or complex MIME messages.

### _smtpd_ Module

The [smtpd](https://docs.python.org/3.5/library/smtpd.html){:target="_blank"} offers several classes to implement SMTP servers.

```python
#!/usr/bin/env python3

import smtpd
import asyncore

class ZhuSMTPServer(smtpd.SMTPServer):

    def process_message(self, peer, mailfrom, rcpttos, data):
        print("Receiving message from:", peer)
        print("\taddress from:", mailfrom)
        print("\taddress to:", rcpttos)
        print("\tmessage length:", len(data))

server = ZhuSMTPServer(("127.0.0.1", 40480), None)

asyncore.loop()
```

> A package call [aiosmtpd](http://aiosmtpd.readthedocs.io/){:target="_blank"} is a recommended replacement for this module. It is based on asyncio and provides a more straightforward API. smtpd should be considered deprecated.


## Other Application Protocols

Here are some other application protocols whose clients can be developed in Python.

### Telnet

Telnet is a protocol used on the Internet or local area network to provide a bidirectional interactive text-oriented communication facility using a virtual terminal connection.

The [telnetlib](https://docs.python.org/3.5/library/telnetlib.html){:target="_blank"} module provides a Telnet class that implements the Telnet protocol.

```python
#!/usr/bin/env python3

import telnetlib

HOST = "xmltrek.com"
PORT = 1701

tn = telnetlib.Telnet(host=HOST, port=PORT)

tn.read_until(b"Ship name: ")
tn.write("sampig".encode("ascii") + b"\n")
tn.read_until(b"Player: ")
tn.write("zhuzhu".encode("ascii") + b"\n")

...

print(tn.read_all().decode("ascii"))
tn.close()
```

### NNTP

The NNTP (Network News Transfer Protocol) is an application protocol used for transporting Usenet news articles between news servers and for reading and posting articles by end user client applications.

The [nntplib](https://docs.python.org/3.5/library/nntplib.html){:target="_blank"} module defines the class NNTP which implements the client side of the Network News Transfer Protocol. It can be used to implement a news reader or poster, or automated news processors.

Some parts of the codes:
```python
#!/usr/bin/env python3

import nntplib

s = nntplib.NNTP('news.gmane.org')
resp, count, first, last, name = s.group('gmane.comp.python.committers')
print('Group', name, 'has', count, 'articles, range', first, 'to', last)

resp, overviews = s.over((last - 9, last))
for id, over in overviews:
    print(id, nntplib.decode_header(over['subject']))

s.quit()
```

### IRC

The IRC (Internet Relay Chat) is an application layer protocol that facilitates communication in the form of text.
[IRC](http://www.irc.org/tech_docs/rfc1459.html){:target="_blank"} protocol contains several messages or commands:
1. Command: `USER`<br/>
Parameters: `<username> <hostname> <servername> <realname>`
2. Command: `NICK`<br/>
Parameters: `<nickname> [ <hopcount> ]`
3. Command: `SERVER`<br/>
Parameters: `<servername> <hopcount> <info>`
4.  Command: `JOIN`<br/>
Parameters: `<channel>{,<channel>} [<key>{,<key>}]`
5. Command: `PRIVMSG`<br/>
Parameters: `<receiver>{,<receiver>} <text to be sent>`

It is possible to use `socket` module to develop an application for IRC client.

```python
#!/usr/bin/env python3

import socket

...
irc = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
irc.connect(("SERVER", 6667))
irc.send("USER " + username + " " + hostname +" " + servername + realname + "\r\n")
...
irc.send("NICK " + nickname + "\r\n")
irc.send("JOIN " + channel + "\r\n")
# send message:
# irc.send("PRIVMSG " + receiver + " " + text + "\r\n")
# receive message:
# text = irc.recv(1024)
```


## References

1. [Python Official Documentation](https://www.python.org/doc/){:target="_blank"}
2. [Internet Protocols and Support](https://docs.python.org/3.5/library/internet.html){:target="_blank"}
