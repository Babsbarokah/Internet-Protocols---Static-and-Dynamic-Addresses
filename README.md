# Internet-Protocols---Static-and-Dynamic-Addresses
Troubleshooting and analyzing the difference between a statically and dynamically assigned IP addresses using EC2 instances.

## Project Overview
As a Cloud Support Engineer, I investigated a networking issue related to dynamic and static IP addresses in AWS. A customer reported that their EC2 instance's IP address changed each time the instance was stopped and started, causing disruptions in their infrastructure. My task was to analyze and resolve the issue by assigning a persistent (static) IP to the instance.

<img width="896" alt="Screenshot 2025-03-23 at 23 15 03" src="https://github.com/user-attachments/assets/dd89f6f9-c03b-44ae-9159-7d7ea3153a78" />

Image: customer's architecture

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

<img width="1439" alt="Screenshot 2025-03-23 at 23 30 20" src="https://github.com/user-attachments/assets/5ee19c92-deb9-42b8-9d3b-770fc87f6e6b" />

---

### Key Observations:
- Public IPs assigned to EC2 instances by default are dynamic and change upon instance restart.
<img width="1438" alt="Screenshot 2025-03-23 at 23 34 14" src="https://github.com/user-attachments/assets/95620363-48e5-4c37-88a8-a0c82cc8ddfb" />

 
--- 
- Private IPs remain the same within the VPC but are not accessible from the internet unless mapped to a public IP.

<img width="1438" alt="Screenshot 2025-03-23 at 23 38 04" src="https://github.com/user-attachments/assets/2f4258f7-080f-4d23-8bb6-ff73a252a6a3" />

--- 
  
- AWS provides Elastic IPs (EIPs) to assign static public IPs to instances, ensuring persistent connectivity.

  <img width="1438" alt="Screenshot 2025-03-23 at 23 43 33" src="https://github.com/user-attachments/assets/695661f8-c98e-4be0-9c1d-81425ccd4bd1" />


## Solution Implementation
To resolve the issue, I allocated and associated an Elastic IP with the EC2 instance:
1. **Allocated an Elastic IP** via the EC2 dashboard under *Network & Security > Elastic IPs*.

<img width="1440" alt="Screenshot 2025-03-23 at 23 39 35" src="https://github.com/user-attachments/assets/256032a6-2236-448e-980e-30ed37c85925" />

<img width="1432" alt="Screenshot 2025-03-24 at 00 11 16" src="https://github.com/user-attachments/assets/09fd59e3-7269-4d1e-a409-0c8ce00e6220" />


--- 
2. **Associated the Elastic IP** with the problematic EC2 instance.

<img width="1438" alt="Screenshot 2025-03-23 at 23 43 33" src="https://github.com/user-attachments/assets/cbfdd910-44ee-4d48-b1e8-f3878b061be8" />


--- 
3. **Validated the fix** by stopping and starting the instance to confirm that the public IP remained unchanged.

<img width="793" alt="Screenshot 2025-03-23 at 23 54 40" src="https://github.com/user-attachments/assets/e2a8fcde-7e61-4e68-8a0c-0c040e25ecf6" />

--- 

<img width="800" alt="Screenshot 2025-03-23 at 23 55 29" src="https://github.com/user-attachments/assets/893409b2-c221-4407-9c09-af9e34aa264f" />


### Final Outcome
After associating an Elastic IP, the instance retained its public IP across stops and starts, successfully resolving the issue for the customer. James’s infrastructure remained stable without further disruptions.

## Conclusion
By associating an Elastic IP with the instance, I ensured that the public IP remained constant, resolving the customer’s issue. This hands-on troubleshooting experience reinforced my understanding of AWS networking concepts, specifically static vs. dynamic IP assignments within EC2.


### Key Learnings:
I learned that AWS assigns dynamic public IPs that change when an instance restarts. Elastic IPs provide a static public IP that stays the same. Troubleshooting is most effective when replicating the issue before applying a fix.


---



