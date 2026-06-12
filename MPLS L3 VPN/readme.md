In this project, we have two customers (Site-A and Site-B), and they send traffic across an ISP backbone. But these two customers never see each other's data. 

The ISP creates a separate "virtual mailbox" (called a VRF) on each edge router. Each customer's traffic gets wrapped in two labels, namely outer label and inner label. The outer label that tells the core routers where to send the packet, whereas the inner label that tells the edge router which customer it belongs to. 

When the packet arrives, the inner label is stripped off and the packet is delivered to the correct customer. And so, we are proving how ISPs offer private network services to enterprise customers without building separate physical networks.