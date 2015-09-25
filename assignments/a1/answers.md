---
title: CSC 463 A1
author: Andrew Hobden (V00788452)
---

## Question 1

### Q1.A

In the "EE" model we noted:

$$\frac{ P_{xy} }{ \sum_{i \neq x}{ P_{iy} } } \geq \beta$$

In this problem we set $\beta = 1.25$. Since transmission power is the same for each node we set this to $1$.

Where $P_r(d) = \frac{P_t}{d^2}$.

* $1 \rightarrow 2$
    $$\frac{ P_{12} }{ P_{52} + P_{62} } = \frac{ \frac{1}{1^2} }{ \frac{1}{(\approx 2)^2} + \frac{1}{(2)^2} } = \frac{ 1 }{ (\approx \frac{1}{4}) + \frac{1}{4} } \approx 2 \geq \beta$$
* $5 \rightarrow 8$
    $$\frac{ P_{58} }{ P_{18} + P_{68} } = \frac{ \frac{1}{1^2} }{ \frac{1}{(\approx 2.8)^2} + \frac{1}{(2)^2} } = \frac{ 1 }{ (\approx .1275) + \frac{1}{4} } \approx 2.649 \geq \beta$$
* $6 \rightarrow 7$
    $$\frac{ P_{67} }{ P_{17} + P_{57} } = \frac{ \frac{1}{1^2} }{ \frac{1}{(\approx 2)^2} + \frac{1}{(\sqrt{2})^2} } = \frac{ 1 }{ (\approx \frac{1}{4}) + \frac{1}{2} } \approx \frac{4}{3} \geq \beta$$

$\therefore$ The maximal number of simultaneous transmissions is $3$.

### Q1.B

In the "CS Model" we note that, for example, if $1$ is transmitting $2$ and $4$ will both receive the transmission. If they are receiving another transmission at the same time this will collide.

Thus, if $1 \rightarrow 2$ then $1 \rightarrow 4$ as well. This means $4$ cannot receive data from any other node.

One solution to the maximal simultaneous network transmissions is:

* $1 \rightarrow 2$
    - $3$ cannot send data without clobbering $2$'s received data.
    - $4$ cannot receive data since $1$'s sent data would clobber it.
* $5 \rightarrow 8$
    - $3$ receives the data, but this does not effect the system.
    - $7$ cannot send data without clobbering $8$'s received data.
* $6 \rightarrow 7$
    - $4$ receives the data, but this does not effect the system.

$\therefore$ The maximal number of simultaneous transmissions is $3$.


## Q4

| Sender  | Reciever | Probability |
|:-------:|:--------:|:-----------:|
| E       | A        | 0.5         |
| E       | B        | 0.2         |
| E       | C        | 0.2         |
| E       | D        | 0.1         |
| A,B,C,D | E        | 0.6         |
| A,B,C,D | A,B,C,D  | 0.4         |
