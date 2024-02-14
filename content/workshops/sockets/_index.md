---
title: "Get Connected - An Intro to Socket Programming in Python"
date: 2024-02-14T16:28:36Z
draft: true
outputs: [Reveal]
---

{{% note %}}
## Editorial Decisions

- Only focus on AF_UNIX and AF_INET. Why?
    - These are the overwhelming majority of socket domains.
    - The point of the workshop is to get attendees familiar with the concept of sockets themselves not the particulars of specific domains.
    - AF_INET6 can be safely ignored since IPv6 is not *fundamentally* different from IPv4 and I do not want to go into digressions on `flowinfo` and `scope_id`.
- Use Python. Why?
    - With C I will have to go in to multiple digressions on what file descriptors are, what C-strings are, what network-byte order is, etc. With Python I can keep the workshop focussed on sockets themselves.
    - The Python API is *much* cleaner.
    - More people are going to be familiar with Python than with C.
    - Less platform-specific concerns; there are going to be people at the workshop with Windows machines.
    - {{% /note %}}

# Sockets

--------

## IPC: Inter-Process communication

- **note:** it is the *processes* that are communicating, *not* the hosts/machines.
- same host OR different host

- Near-universal method of IPC
    - First implemented in 1983 with 4.2BSD
    - has since been ported to virtually every operating system

57 - domain sockets - same host IPC
59 - internet domain sockets - different host IPC
60 - server design

--------

## Sockets

Both sides (client/server or communicator/communicatee)
server should *bind* socket to a well known address so that clients can locate it
    - does not apply to p2p communication

Sockets exist in a communication domain, which determines -
    - the method of identifying a socket (i.e., the format of a socket “address”); and
    - the range of communication (i.e., either between applications on the same host
        or between applications on different hosts connected via a network)

Exact domains supported vary by OS. But these three are almost-universally supported and are the most essential -
    - AF_UNIX sockets - for same-host communication
    - AF_INET - for different-host communication
    - AF_INET6 - same as AF_INET, but uses IPv6 addresses

AF_UNIX - in-kernel - two programs on the same host - pathname
AF_INET - network - two programs on different hosts - IPv4 address
AF_INET6 - network - two programs on different hosts - IPv6 address

Sockets are in two types - stream/datagram
    stream - connection-oriented with reliable delivery. message boundaries not preserved
    datagram - connection less without reliable delivery. message boundaries preserved

[Image here to illustrate difference between stream and datagram sockets]
