# Toward an SDN-Enabled NFV Architecture

- Authors:
	- Jon Matias, Jokin Garay, Nerea Toledo, Juanjo Unzilla, and Eduardo Jacob
- Published In:
	- IEEE Communications Magazine ( Volume: 53, Issue: 4, April 2015 )	

---

# Overview

- Introduction
- Toward An SDN-Enabled NFV Architecture
- FlowNAC: A Real Experience Exploring  Novel NFV Architectures
- Issue and Chanllenge
- Conclusion

---

# Introduction

- SDN has also contributed to the virtualization of the network infrastructure
	- providing the foundation to isolate, abstract, and share the network resources
- Virtualized network functions (VNFs)
	- compose the service chain
	- basic elements to achieve the complete virtualization of service delivery and are commonly based on computing resources

---

# Introduction

- In this article we try to clarify the evolution of SDN & NFV relationship in the context of service provisioning.
- A real example, FlowNAC
	- to illustrate the applicability of NFV using different architectures and the advantages offered by the SDN-enabled NFV approach in service provisioning scenarios.

---

# Toward An SDN-Enabled NFV Architecture

- Goal: Enable dynamic deployment of NFVs
- Requirement: 
	- support multi-tenancy
	- multiple service chain share same physical resource
	- traffic steering between VNFs must be isolated
- SDN is perfect to deal with these requirement.

---

# Toward An SDN-Enabled NFV Architecture

- SDN provide network infrasctructure with enhance capababilities to improve how VNF are designed
- The three evolution steps of their relationship are
	- SDN-agnostic NFV architecture
	- SDN-aware NFV architecture
	- SDN-enabled NFV architecture

---

## SDN-agnostic NFV architecture

- NFV
	- First step fot enable the decoupling of software from hardware
	- Each VNF is a software box to process traffic from underlying network
- NFV Infrastructure (NVFI)  
	- Just providing connectivity
	- Limited to providing interface to the underlying network resources

---

## Related Work of SDN-agnostic architecture 

- ETSI ISG for NFV
	- "ETSI GS NFV 002: Network Functions Virtualisation (NFV); Architectural Framework", 2015
	- "NFV Proofs of Concept", 2015

---

## SDN-aware NFV architecture

- NFV
	- Process all data traffic
- NFVI
	- Support interface to control
	- Only provide connectivity with enhanced capabilities, such as dynamic control and configuration
- Related Work:
	- ONF, “OpenFlow-Enabled SDN and Network Functions Virtualization”, 2015

---

## SDN-enabled NFV architecture

- Based on this programmability of NFVI 
	- The network infrastructure layer to may become a part of implementating the VNF
- Advantages
	- data traffic performance
	- wider placement scope
	- better resource utilization, to avoid traffic going up to and down from a VM to process the frames

---

## VNF Design Consideration

- Which is the best way to combine compute and network resource to implement VNFs?
- There are three processing type of VNF
	- stateless
	- limited or light-weight state
	- stateful

---

## VNF Design Consideration

- Stateless
	- Previously matched frames **do not affect** subsequent frames
- Limited or light-weight state
	- State can be kept in the data path, such as flow-level counters, timers for flow expiration, and queue-level counters 
- Stateful
	- Processing of each packet is not independent

---

##  VNF Design Consideration

- Design Goal:
	- The stateful component is based on virtual compute resources to keep the state associated with the VNF
	- The stateless component makes use of SDN datapath resources to perform data traffic processing efficiently. 
- The main idea is to keep data processing in hardware as much as possible, and only forward the data traffic to the stateful component when the processing is also stateful.

---

##  VNF Design Consideration

![inline](https://raw.githubusercontent.com/vicky-sunshine/my-paper-record/master/Toward-SDN-enabled-architecture/img/Fig2_SDN_based_component.png)

---

##  VNF Design Consideration

- There are also three ways to implement VNFs
	- solely with compute resources 
	- solely with network resources
	- splitting the design following the aforementioned separation of stateful and stateless components

- Each of the options is best suited for a different scenario, related to 
	- the data processing speed requirement
	- the complexity of the state to be kept

---

##  VNF Design Consideration

![inline](https://raw.githubusercontent.com/vicky-sunshine/my-paper-record/master/Toward-SDN-enabled-architecture/img/Table1_VNF_design.png)

---

## Toward An SDN-Enabled NFV Architecture

![inline](https://raw.githubusercontent.com/vicky-sunshine/my-paper-record/master/Toward-SDN-enabled-architecture/img/Fig1_NFV_archi_evolution.png)

---

## FlowNAC

- Traditional network access control
	- based on physical port of network node
- FlowNAC is flow-based network access control solution
	- based on flow (defined by OpenFlow)
- Use this scenario to demonstrate new NFV architectures

---

## FlowNAC: type of traffic

- a-type: 
	- Authentication and authorization (AA)
	- Must be processed by VNF to keep the state associated with each AA process.
	- Being related to the AA process, it will be limited in time and volume

---

## FlowNAC: type of traffic

- b-type
	- Authorized data traffic
	- Must be granted access to the network
- c-type: 
	- Non-authorized data traffic
	- Must be denied access to the network. 

---

## FlowNAC with SDN-agnostic/aware Architecture

- One VNF block handle all traffic (both AA and data traffic)
	-  all data traffic send to VNF block
	-  VNF block handle AA data and decide which data traffic is allowed

- problems:
	- relies on solely computer resources
	- scalability would be limited by the availability of computing resources.

---

## FlowNAC with SDN-enabled Architecture

- AA block
	- keeps the state of the AA process currently excuted
	- computer resource
- Access control enforcing block
	- limits the access only to already authorized services and does not require any state
	- networking device

--- 

## FlowNAC with SDN-enabled Architecture

- Only AA traffic is sent to the AA block to be processed and SDN switch is configured by the result of AA process
- Authorized and unauthorized data traffic is processed by the SDN switch
    - Authorized traffic is allowed
    - Unauthorized traffic is drop

---

# FlowNAC with SDN-enabled Architecture

- computer resource only need to handle AA traffic and authorized data traffic
- networking resources used for the access control (cost most time)
- Advantages
	- data processing speed of VNF is imporved
	- reducing general network utilization

---

# Issue and Challenge

- VNFs designed also employing network elements **add complexity** to the optimal placement decision. 
- The NFV framework must now orchestrate an additional type of resource with **its own constraints** (e.g., the rule insertion performance or flow table size).

---

# Conclusion

- The processing of network packets is partially **offloaded** to the network element (the SDN switch) while maintaining the stateful processing of the VNF on the compute element.
	