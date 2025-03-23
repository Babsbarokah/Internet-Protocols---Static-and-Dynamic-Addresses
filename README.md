# Internet-Protocols---Static-and-Dynamic-Addresses
Troubleshooting and analyzing the difference between a statically and dynamically assigned IP addresses using EC2 instances.

## Project Overview
As a Cloud Support Engineer, I investigated a networking issue related to dynamic and static IP addresses in AWS. A customer reported that their EC2 instance's IP address changed each time the instance was stopped and started, causing disruptions in their infrastructure. My task was to analyze and resolve the issue by assigning a persistent (static) IP to the instance.

## Scenario
A Fortune 500 company's Cloud Administrator, James, submitted a support request regarding an EC2 instance losing its IP address upon restart. The customer’s architecture included a Virtual Private Cloud (VPC), an Internet Gateway, a public subnet, and an EC2 instance. James needed a static IP for the instance to prevent breaking dependencies on other resources.

### Customer's Support Request
> *Hello Cloud Support!*
>
> *We are having issues with one of our EC2 instances. The IP changes every time we start and stop this instance, causing everything to break since it requires a static IP address. We are unsure why this happens. Could you investigate? Attached is our architecture.*
>
> *Thanks!*
>
> *James, Cloud Admin*

## Investigation and Analysis
I reviewed the customer's setup and replicated the issue by launching an EC2 instance with default settings. When stopping and starting the instance, the public IPv4 address changed, confirming that the instance had a dynamic public IP. However, the private IPv4 address remained unchanged, indicating it was assigned dynamically within the VPC.

### Key Observations:
- Public IPs assigned to EC2 instances by default are dynamic and change upon instance restart.
- Private IPs remain the same within the VPC but are not accessible from the internet unless mapped to a public IP.
- AWS provides Elastic IPs (EIPs) to assign static public IPs to instances, ensuring persistent connectivity.

## Solution Implementation
To resolve the issue, I allocated and associated an Elastic IP with the EC2 instance:
1. **Allocated an Elastic IP** via the EC2 dashboard under *Network & Security > Elastic IPs*.
2. **Associated the Elastic IP** with the problematic EC2 instance.
3. **Validated the fix** by stopping and starting the instance to confirm that the public IP remained unchanged.

### Final Outcome
After associating an Elastic IP, the instance retained its public IP across stops and starts, successfully resolving the issue for the customer. James’s infrastructure remained stable without further disruptions.

## Conclusion
By associating an Elastic IP with the instance, I ensured that the public IP remained constant, resolving the customer’s issue. This hands-on troubleshooting experience reinforced my understanding of AWS networking concepts, specifically static vs. dynamic IP assignments within EC2.


### Key Learnings:
I learned that AWS assigns dynamic public IPs that change when an instance restarts. Elastic IPs provide a static public IP that stays the same. Troubleshooting is most effective when replicating the issue before applying a fix.


---



