# Discussion Questions:

## Paper 1: Performance Evaluation for Hybrid IEEE 802.11b and IEEE 802.11g Wireless Networks

http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.110.9052&rep=rep1&type=pdf

### Q1: What are main differences between IEEE 802.11g and IEEE 802.11b? Are they using the same DCF protocol?  

Maximum transmission rate (54 for g, 11 for b).

Difference | 11b | 11g
-----------|-----|----
Throughput | 11  | 54
Slot Time  | 20  | 9
CW         | 31  | 15

### Q2: How is IEEE 802.11g made compatible with IEEE 802.11b? Why does the solution for compatibility create significant overhead to the network?

If 11g transmits then 11b cannot decode. So 11g has a Protection Window preample that includes information about how long the channel will be busy.

### Q3: Check the parameter settings in Table 2. When an IEEE 802.11b STA compete with an IEEE 802.11g STA, which node has a better chance to win the competition and capture the channel?

G has a better chance since the CW and slot times are smaller.

### Q4: Check Figure 3. Why the throughput of IEEE 802.11b STAs and IEEE 802.11g STAs have similar throughput?

B dominates the throughput since the data rate is slower.

### Q5: Why the throughput of 802.11b STAs in the hybrid network becomes even higher than in a pure all 802.11b network?  

In the pure network the 11B device is limited to 11MBps but in the hybrid network the 11B device is more likely to reach it's max.

### Q6: Comparing Figure 3 to Figures 4 and 5, what cause the different performance results? Why does this phenomenon happen?

Figure 4: When the data packet size gets smaller then the transmission cycle ratio becomes closer to 2/1 which means that B won't dominate as much as it did before. (See section 5.3)

Figure 5: Same general principle holds for this as well. (See section 5.4)

### Q7: What do Figure 6(a), (b), (c) tell you?

See section 6.

## Paper 2:  Can CSMA/CA networks be made fair

http://www.cise.ufl.edu/~yjian/MobiCom08-Jian.pdf

### Q1: Check IEEE 802.11 specification, under what condition EIFS should be used? Check IEEE 802.11, Section 9.2.10 and find how long EIFS should be.

EIFS = SIFS + DIFS + ACK, used when there is a frame drop.

### Q2: Check Figure 1 and Figure 2, explain why the two flows have different throughput when the distance between b and c changes?

When BC are close then A is sensing D transmitting and seeing corrupted packets, so it waits EIFS.

The rest of the answer was unintelligible.

### Q3: Why does overhearing-based solutions not working well?

If you're outside of the sensing range you'll get sparse data, also hidden terminal etc.

### Q4: What is AIMD? Why does the mechanism AIMD works fine for TCP but not for CSMA/CA?

Additive Increase, Multiplicative Decrease. Basically TCP without slow start.

It's hard to use this in CSMA since we don't know the status of the network at any given time since we might now see all the nodes. We just don't have enough information to pull this off in CSMA/CA.

### Q5: What is the proposed solution in the paper? Describe the basis idea.

Proposed solution to detect congestion is to send "important" packet fragments to the network encouraging the other nodes on the network to believe there is congestion. After two time slots it stops this and does a multiplicative decrease. The other nodes will also see congestion and decrease as well.

### Q6: What might be the problems in the proposed solution?

* The network gets flooded to syncronize a decrease, but causes temporary uselessness.
* Fairness
* Not tested on variable loads.
