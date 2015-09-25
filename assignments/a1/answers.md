---
title: CSC 463 A1
author: Andrew Hobden (V00788452)
---

## Question 1

### Q1.A



### Q1.B

In the "CS Model" we note that, for example, if $1$ is transmitting $2$ and $4$ will both receive the transmission. If they are receiving another transmission at the same time this will collide.

Thus, if $1 \rightarrow 2$ then $1 \rightarrow 4$ as well. This means $4$ cannot receive data from any other node.

One solution to the maximal simultaneous network transmissions is:

* $1 \rightarrow 2$
    * $3$ cannot send data without clobbering $2$'s received data.
    * $4$ cannot receive data since $1$'s sent data would clobber it.
* $5 \rightarrow 8$
    * $3$ receives the data, but this does not effect the system.
    * $7$ cannot send data without clobbering $8$'s received data.
* $6 \rightarrow 7$
    * $4$ receives the data, but this does not effect the system.

$\therefore$ The maximal number of simultaneous transmissions is $3$.
