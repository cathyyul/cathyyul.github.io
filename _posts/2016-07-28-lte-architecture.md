---
layout: single
title: LTE system series \#1 -- system architecture overview
categories: LTE
tag:
- Learning-notes
- LTE
---

As I recently start to follow 5G research, I feel that it is time to review the basics of LTE and therefore has started to do a literature review. I've been collecting notes and figured it will be helpful at least for myself to share some of the materials. As a networking and computer science person, I will focus more on the network architecture and protocols above MAC layer in this series, and in the mean time may try to outline some of the basic concepts at PHY layer to the extent that I judge helpful for the overall understanding of the system.

Now, let's jump in to the high level architecture.

# High level architecture

![High level architecture]({{site.url}}/images/LTE-basic-arch.png){: .center-image }

LTE is a telecommunication network system that is established by a network operator. The architecture is defined by 3GPP. The standard is a combination of physical components and a logical network. Generally, all interfaces except the one between the mobile, i.e. the "UE", and the base station, i.e. the "eNB", are logical interfaces which can be implemented as a link in overlay network.

The high-level system consists of two major components, which are:

- Evolved Packet Core (EPC): often referred to as core network, which takes care of internal packet routing and most control plane functions such as QoS control, traffic accounting, traffic routing to the base stations.

- Evolved Universal Terrestrial Access Network (E-UTRAN): generally defined the Radio Access Network (RAN), which includes the base stations and interfaces to mobiles.

- User Equipment (UE): these are the mobile devices on the networks. Most commonly seen are smartphones nowadays, but there are also other types of UEs such as laptop mobile interface card, or other devices such as cellular version kindles.

The UE, through E-UTRAN and EPC, can connect to Packet Data Networks (PDN). A PDN can be considered as an instance of network, e.g., the Internet or a voice service network. From the LTE network's perspective, these PDNs are the services a UE tries to access through it, and therefore is the external world.

Officially, the whole system is called an Evolved Packet System (EPS), and the term LTE refers to he E-UTRAN part of the standard. However, in common usage, LTE is usually used to refer to the whole system.

Next let's look at the basic architecture of each component.

# UE

## Architecture

![UE Architecture]({{site.url}}/images/UE-arch.png){: .center-image }

The left part of the above figure shows the technical components of a UE. A UE consists of:

- ME: Mobile Equipment. This is the actual communication device, e.g. smartphone. Within an ME, there are two components.
    - MT: Mobile Termination, which handles all the communication functions.
    - TE: Terminal Equipment, which terminates the data streams
- UICC (Universal integrated circuit card): a smart card, i.e. the SIM card
    - It runs an application known as USIM (universal subscriber identity module)
    - USIM stores user specific data, e.g. phone number and home network identity
    - USIM does some security calculation

Although we won't get into the details, it is worth noting how an interface is represented. In the above figure, there is an interface R between TE and MT, and an interface Cu between MT and UICC. When an interface appears on the diagram like this, it means the standard specifies these interfaces and clearly define what message exchanges and protocols are supported between two components as necessary for the system to work.

A LTE UE may support IPv4 and IPv6. Once connected, the UE receives 1 IP address for each PDN it connects to and therefore can use IP stack to communicate with the particular external network.

## UE capabilities

An UE is a device, and vendors may choose to build a selected set of features in a device. Therefore, UE needs to be able to tell the network functions it support. The functions are described by
UE capabilities. The UE capabilities cover issues such as

    - Max data rate it can handle
    - Types of radio access technology that it supports
    - Carrier frequencies
    - Optional features

For simplicity, most important capabilities are grouped into UE category. For example, we may hear someone say a UE is category 5 which means a specific set of parameter values are supported, e.g. the max downlink data rate is 300Mbps and max uplink data rate is 75Mbps for the UE. More details about the specific parameters of UEs can be found on [3GPP website][3gpp-ue-categories].

# E-UTRAN

## Architecture
![RAN Architecture]({{site.url}}/images/RAN-arch.png){: .center-image }

The E-UTRAN covers the access network architecture between the base station, i.e. the eNB in LTE spec, and the UE. An eNB may contain multiple cells. A cell is a sector of the 360 degree area that eNB antenna sets cover. In general, a UE communicates with just one base station and one cell at a time. The interface between UE and eNB is called Uu, as shown in the figure.

Below lists the some most basic concepts about the eNBs.

- Sends radio transmission to mobiles (DL) and receives transmissions from mobiles (UL)
- Controls the low level operation of UEs by sending signalling messages to the UE
- Connect to EPC by S1 interface
- Connect to other eNBs by X2. X2 interface is optional as the connectivity can be achieved by passing messages between eNBs through the EPC with 2 S1s. X2 is mainly used to reduce the latency for signalling and packet forwarding at handover.
- As previously described, S1 and X2 are usually not direct physical connections. They are usually routed by constructing an IP overlay. In other words, the S1 and X2 are logical relationships.

# EPC
![EPC Architecture]({{site.url}}/images/CN-arch.png){: .center-image }

The EPC is the most complicated component in the system, as there are many control and routing functions that are covered deep in the operator network. The diagram above is a simplified version that only shows the most important components.

- Home Subscriber Server (HSS): HSS is the central database containing information about all subscribers
- Packet Gateway (P-GW): This is the EPC’s point of contact with outside world, i.e. the PDN.
    - Each packet data network is identified by an Access point name (APN)
    - Each mobile is assigned to a default PGW when switches on
    - A mobile may be assigned to 1 or more additional PGWs if it connects to other data networks
    - P-GW is the last hop of outgoing user data packets and the first hop of incoming user data packets.
- Serving Gateway (S-GW): High level router that forwards data b/t BS and PGW
    - Typically a network contains a handful SGWs. Each looks after the mobile in a certain geographical region.
- Mobility Management Entity (MME):
    - MME is like the brain of the network. It controls the high level operation of the mobile by sending signaling messages about issues that are unrelated to radio communications, e.g. security, management of data streams
    - MME also controls other elements of the network by signalling internal to EPC

Generally speaking, the MME is a control plane function and SGW is a user plane function. The reason to split these two components is obvious today, but was an advancement a decade ago when LTE network was defined. The two entities used to be one in 3G, which is the only entity that directly talks to the RAN. The separation of user and control plane functions allows the operator to scale the network in response to increasing load. For example, it can add more SGWs for load balancing as the data traffic grows without adding MME, and add more MMEs as the number of UE to control grows. Due to historical reasons, the interface from eNB to MME is called S1-MME and from eNB to S-GW is S1-U.

[3gpp-ue-categories]: http://www.3gpp.org/keywords-acronyms/1612-ue-category
