---
layout: single
title: Modeling a point to point transmission link
categories: Networking
tag:
- Networking
- Simulation modeling
---

Point to point link model is very frequently used in simulating simple networks where two devices are connected by a wired link. Sometimes, it is even used for modeling simplified wireless link model.

When describing a simple point to point link, we define a link has a data rate `R` and a delay `d`. This means the link should be able to transmit at most `R` amount of data in a unit time, and each bit should reach the other end after a time `d`.

Let's take a more concrete example. Say a link has 5Gbps data rate, and 10ms delay (`R`=5Gbps, `d`=10ms). The link should be able to sent out 5 gigabits of data every second, and each bit will reach the receiving end 10ms later after it is sent by the transmitter.

Now, how do we simulate a point to point link?

Network simulators are mostly event based. In order to program this simple model, we need to figure out the time of two events for a packet: the time a packet is sent by a transmitter, and the time this packet is received by the receiver. When a packet comes in to our simulated device for transmission, we need to figure out when the packet can be sent, and when it is fully received by the receiving device.

Let's start from the transmission start time of a packet. When the first packet arrives at the transmitting device, it can be sent immediately. Let's say this time is `T1`. When does this packet reach the other end? You may think the delay is `d`, so the packet reaches the receiver at `T1 + d` second. It's close but not entirely correct.

Why? We can assume the first bit of a packet reaches the receiver at `T1 + d` second, but the packet is not just 1 bit. The receiver fully receives a packet only if it receives all bits of a packet.

When can the last bit be received? To answer this question, we can think about when the last bit is sent. This is where the data rate comes in. The definition of data rate is it is how many bits can be sent in one second. The inverse of the data rate is how much gap time the transmitter needs between one bit to the next. Therefore, assuming our first packet has a length `L1` bits, the device finishes the transmission at time `L1/R`. This is called the transmission delay. In contrary, `d` is called propagation delay, that is, the time a bit needs to travel through the media. Putting everything together, we have, for a packet that is sent at time `T1`, the time the last bit reaches the other end is `T1 + L1/R + d`.

Now let's move on to the second packet.

Assuming the second packet arrives at time `T2`. There are two cases we need to consider:

1. `T2 > T1 + L1/R`: This means packet 2 arrives at the transmitter device after the device is done with the previous packet. So we can send the packet right away at `T2`. The time packet 2 reaches the receiver is `T2 + L2/R + d` (assuming packet 2's size is `L2`) in this case.
2. `T2 <= T1 + L1/R`: The second packet may arrive before we finish transmitting the first packet. In this case, the second packet has to wait until the transmitting device finishes transmitting the first packet. The point is it's the time finish "transmitting" the packet instead of receiving. After transmitting all `L1` bits of packet 1, the transmitter becomes available to send the first bit of the second packet. So the time we can start transmitting the second packet is `T1 + L1/R`. There is no `d` portion in this calculation because the time `d` is the time the bits are in the air. The transmitter device can become available before the previous packet actually reaches the receiver.

The same logic follows for all subsequent packets. Any packet falls in one of the two cases below based on its arrival time:
- Case 1: the subsequent packet arrives after the previous packets have all been sent
- Case 2: the subsequent packet arrives before the previous packets have been sent. It has to wait until all previous packets are out.

Put it in another way: generally, all arriving packets first enter a transmission queue. If the queue is empty when the packet comes in, the packet can leave the queue immediately. Otherwise, the packet stays in the queue until all previous packets exit the queue. For the ease of computation, imagine the "previous packets" in the queue is a giant aggregated packet whose length is the sum of all individual packets being sent out immediately. The size of this giant packet is the "state" of queue `Q`. When a packet with length `l` arrives at a queue whose state is `Q`, the arriving packet will be sent out at `Q/R + d` time from now and this packet will reach the receiver at `Q/R + l/R + d` from now.
