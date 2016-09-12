## Toward an SDN-Enabled NFV Architecture


---

## Overview
- Introduction
- Related Work
- Toward An SDN-Enabled NFV Architecture
- FlowNAC: A Real Experience Exploring  Novel NFV Architectures
- Issue and Chanllenge
- Conclusion

---

## Introduction

---

## Related Work

---

## Toward An SDN-Enabled NFV Architecture

- Goal: Enable dynamic deployment of NFVs
- Requirement: 
	- support multi-tenancy
	- multiple service chain share same physical resource
	- traffic steering between VNFs must be isolated
- SDN is perfect to deal with these requirement.

---

## Toward An SDN-Enabled NFV Architecture

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

## SDN-agnostic NFV architecture 
- Related Work
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
- There are three processing complexity of VNF
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

- There are also three ways to implement VNFs
	- solely with compute resources 
	- solely with network resources
	- splitting the design following the aforementioned separation of stateful and stateless components



---

## Issue and Challenge
- VNFs designed also employing network elements add complexity to the optimal placement decision. 
- The NFV framework must now orchestrate an additional type of resource with its own constraints (e.g., the rule insertion performance or flow table size).

---

## Conclusion
- The processing of network packets is partially offloaded to the network element (the SDN switch)  while maintaining the stateful processing of the VNF on the compute element.
