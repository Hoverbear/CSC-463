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

## Question 2

$$d = 0.5 * d_2$$
$$d_3 = 1.5 * d_2$$

Allowing $d$ to be the unit, $d=1$, $d_2=2$, $d_3=3$.

Therefore if nodes $d=1$ distance away from each other, can reliably transmit $d_2=2$ distance units, and can sense $d_3=3$ distance units, then we need to consider that $N_1$ can transmit to $N_2$ or $N_3$ reliably, and $N_4$ would sense this transmission and not be able to receive other transmissions.

So, if $N_1$ transmitted, the next node that could safely transmit would be $N_5$.

$\therefore$ The number of nodes that can transmit is $\frac{n}{5}$.

## Question 3

**Notes:**

* Since the radio channel is *reliable* we don't need to think about $\text{ACK}_{Timeout}$.
* Since the channel is reliable we can assume that the connection always receives the correct 1 Mbps.
* Since there is no *fragmentation* of packets needed we can presume the packet payload size is sufficient for the message for the first, and only, frame in each.
* Referencing figure on page 93 (of PDF http://webhome.csc.uvic.ca/~wkui/Courses/wireless/802.11-1999.pdf) figure 52.
* Assuming both Laptops start listening at the beginning of a DIFS slot.
* Assuming both Laptops will start transmitting at the end of the DIFS, and collide.



**Definitions:**

* **Slot Time:** The Slot Time (in $\mu$s) that the MAC will use for defining the PIFS and DIFS periods.
* **SIFS Time:** The nominal time (in $\mu$s) that the MAC and PHY will require to receive the last symbol of a frame at the air interface, process the frame, and respond with the first symbol on the air
interface of the earliest possible response frame.
* **$CW_{\text{min}}$:** The minimum size of the contention window, in units of `Slot Time`.
* **$CW_{\text{max}}$:** The maximum size of the contention window, in units of `Slot Time`.


### Q3.A

See attached hand-drawn figure.

### Q3.B

Time to transmit frame, as one fragment: $\frac{1024 + 272 + 128 \text{bits}}{ 1,000,000 \frac{\text{bits}}{\text{s}} } = 0.001424 \text{s} = 1424 \mu \text{s}$.
Time to transmit ACK: $\frac{ 112 + 128 \text{bits}}{ 1,000,000 \frac{\text{bits}}{\text{s}} } = 0.00024 \text{s} = 240 \mu \text{s}$

$\therefore$ The first laptop will have successfully transmitted after the following events:

* DIFS ($128 \mu$s)
* (Sent, Collided) DATA ($1424 \mu$s)
* DIFS ($128 \mu$s)
* ACK Timeout ($300 \mu$s)
* DIFS ($128 \mu$s)
* Backoff ($n*50 \mu$s)
* DIFS ($128 \mu$s)
* (Sent) DATA ($1424 \mu$s)
* SIFS ($28 \mu$s)
* (Recieved) ACK ($240 \mu$s)

The expected delay for one laptop to successfully transmit it's first packet is dependent on the backoff chosen, represented as $n*50 \mu$s where $n$ is a randomly generated number.

We will assert that the desired answer requires that the laptop receive an ACK back.

$\therefore$ The expected delay is:

$$ 128*4 + 28 + 1424*2 + 300 + 240 + 50*n = 3928 + 50n \mu\text{s}$$

## Question 4

$$E_{Tx}(d)=c(d^2)$$
$$E_{Total}=E_{Tx}(d)+E_{Rx}=c(d^2)+E_{Rx}$$

**Notes:** Because it is not noted otherwise,

* We consider $E_{Rx}$ to be a constant.
* We assume $E_{Rx}$ is only a cost that the intended receiver pays, not all devices receiving the transmission.
* We assume the distance between nodes $AB$, $CD$, $AD$, $BC$ is $2$.
* $N_i$ denotes a node with ID $i$. $D_{ij}$ is the distance between nodes $i$ and $j$.
* The traffic generated by a node node is $T_i$, however since all are the same $T$ can be used to simplify.

| Sender  | Receiver | Probability |
|:-------:|:--------:|:-----------:|
| E       | A        | 0.5         |
| E       | B        | 0.2         |
| E       | C        | 0.2         |
| E       | D        | 0.1         |
| A,B,C,D | E        | 0.6         |
| A,B,C,D | A,B,C,D  | 0.4         |

<!-- TODO -->

## Question 5

$$ E_{T_x}(d)=cd^\alpha $$

$$ \angle BAC = \theta $$

### Q5.a

$$ d_1 < d_3\cos{\theta} $$

Where $\alpha=2$.

$$ E_{T_x}(d_1) + E_{T_x}(d_2) = cd_1^2 + cd_2^2 = c(d_1^2 + d_2^2) $$

$$ E_{T_x}(d_3) = cd_3^2 = cd_3^2 $$

Showing when $d_1 < d_3 * \cos{\theta}$:

$$  c(d_1^2 + d_2^2) < cd_3^2 $$
$$  d_1^2 + d_2^2 < d_3^2 $$

We note the cosine law of $d_3^2=d_1^2+d_2^2-2(d_1)(d_2)\cos{\theta}$.

$$ d_2 = \sqrt{ d_1^2 + d_3^2 - 2d_1d_3\cos{\theta} } $$

Substituting $d_2$:

$$ d_3^2 > d_1^2 + (d_1^2 + d_3^2 - 2d_1d_3\cos{\theta}) $$

$$ d_3^2 > d_3^2 + 2d_1^2 - 2d_1d_3\cos{\theta} $$

Moving the last LHS term to the RHS:

$$ d_3^2 + 2d_1(d_1 - d_3 \cos{\theta}) > d_3^2 + 2d_1^2 $$

From here we know that $d_3\cos{\theta} > d_1$.

So we know that $d_3^2 + 2d_1(d_1 - d_3 \cos{\theta}) \approx d_3^2 + 2d_1 - n$ **where $n$ is some small value**. (We assert that $2d_1 - n < 2d_1^2$)

Then:

$$ d_3^2 + 2d_1 - n > d_3^2 + 2d_1^2 $$

This shows that:

$$ E_{T_x}(d_1) + E_{T_x}(d_2) < E_{T_x}(d_3) $$

The energy to transmit from $A$ to $C$ directly is more than the energy to transmit from $A$ to $B$ to $C$.

### Q5.b

$$ (\frac{ d_3 }{ d_1 })^\alpha - 1 > (1 + (\frac{d_3}{d_1})^2 - 2(\frac{d_3}{d_1})\cos{\theta})^{\frac{\alpha}{2}} $$

Setting $d_1 = 1$, it becomes:

$$ d_3^\alpha - 1 = ( 1 + d_3^2 - 2d_3\cos{\theta} ) $$

Applying the cosine law to get $d_2$ we get:

$$ d_2^2 = 1^2 + d_3^2 - 2d_3(1)\cos{\theta} $$

Which substitutes into the equation, yielding:

$$ d_3^\alpha - 1 > (d_2^2)^{\frac{\alpha}{2}} $$

$$ d_3^\alpha > d_2^\alpha + 1 $$

Recalling that $d_1 = 1$:

$$ d_3^\alpha > d_2^2 + d_1^2 $$

$\therefore$ The energy to transmit from $A$ to $C$ directly is more than the energy to transmit from $A$ to $B$ to $C$.
