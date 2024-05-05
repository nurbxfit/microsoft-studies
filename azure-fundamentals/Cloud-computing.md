# What is Cloud Computing

Cloud computing is the on-demand delivery of computing services over the internet. These services include common infrastructure like servers, storage, and networking, as well as more advanced offerings like Internet of Things (IoT), Machine Learning (ML), and Artificial Intelligence (AI). Essentially, it allows you to outsource your computing capabilities to a cloud service provider.

**Benefits of Cloud Computing:**

* Cost savings: No upfront investment in hardware and software.
* Scalability: Easily adjust resources up or down as needed.
* Increased productivity: Faster deployment and access to applications.

# Shared Responsibility Model in Azure

In traditional on-premises computing, organizations are responsible for managing and maintaining their entire IT infrastructure, including servers, network devices, software patches, and security.

The cloud computing model with Azure adopts a shared responsibility model. Here's how it breaks down:

* **Microsoft Azure's Responsibility:**
    * Physical infrastructure (hardware, network)
    * Virtualization layer
    * Security of the underlying platform
* **Customer's Responsibility:**
    * Operating system
    * Applications
    * Data
    * Security configuration of their environment within Azure

![Share Responsibility Representation](https://learn.microsoft.com/en-us/training/wwl-azure/describe-cloud-compute/media/shared-responsibility-b3829bfe.svg)


# Cloud Models
Cloud models define how you deploy your cloud resources. 

**There are three main options:**

- **Private cloud**: This is similar to your own data center, but accessible over the internet. It offers high control and security but comes with greater cost and fewer benefits of public clouds. You can host it on-site or in a dedicated off-site data center.

- **Public cloud**:  This is the most common model. Resources are offered by a third-party provider like Microsoft Azure or Amazon Web Services (AWS). Anyone can access and use these resources, making them readily available and cost-effective.

- **Hybrid cloud**: This combines both private and public clouds. You can use the public cloud for temporary spikes in demand or for less sensitive data, while keeping critical applications or highly secure data in your private cloud. This offers a balance between control, security, and scalability.


| Public cloud                                           | Private cloud                                           | Hybrid cloud                                           |
|--------------------------------------------------------|---------------------------------------------------------|--------------------------------------------------------|
| No capital expenditures to scale up                   | Organizations have complete control over resources and security | Provides the most flexibility                          |
| Applications can be quickly provisioned and deprovisioned | Data is not collocated with other organizations’ data | Organizations determine where to run their applications |
| Organizations pay only for what they use              | Hardware must be purchased for startup and maintenance | Organizations control security, compliance, or legal requirements |
| Organizations don’t have complete control over resources and security | Organizations are responsible for hardware maintenance and updates |                                                        |


# Beyond Cloud Models: Multi-Cloud and Management

**There's another option beyond the three main cloud deployment models:**

- **Multi-cloud**: This approach leverages multiple public cloud providers. You might use them for specific features, during migration, or simply for redundancy. Regardless, you manage resources and security across these different environments.

**Here are some tools to help manage complex cloud deployments:**

- **Azure Arc**: This service helps manage your entire cloud environment, regardless of whether it's public (including multi-cloud), private, or hybrid. It provides a unified platform for overseeing resources and security.

- **Azure VMware Solution**: This caters to those already using VMware in a private cloud. It allows you to seamlessly migrate and run your VMware workloads within the Azure public cloud, offering integration and scalability benefits.

# Describe the consumption-based model

## Consumption-Based Model:
- **Definition:** Involves paying for IT resources based on actual usage rather than upfront investment in physical infrastructure.
- **Contrast:** Contrasts with traditional models of IT infrastructure that involve capital expenditure (CapEx) and operational expenditure (OpEx).
- **Benefits:**
  - No upfront costs.
  - Flexibility to scale resources up or down as needed.
  - Efficient cost management, as users only pay for what they use.
  - Eliminates the need to estimate future resource needs accurately.
  - Avoids overprovisioning or underprovisioning issues associated with traditional data centers.
  
## Cloud Pricing Models:
- **Definition:** Cloud computing services are delivered over the internet using a pay-as-you-go pricing model.
- **Advantages:**
  - Helps plan and manage operating costs effectively.
  - Allows for more efficient resource utilization.
  - Enables scalability in line with business requirements.
- **Comparison:** Cloud resources are treated as rented compute power and storage from a provider, eliminating the need for maintenance of underlying infrastructure.
- **Flexibility:** Users can quickly adapt to business challenges and leverage cutting-edge solutions without the overhead of managing physical hardware.
