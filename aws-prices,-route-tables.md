[AWS VPN pricing](https://aws.amazon.com/vpn/pricing/)

**0.05 per Site-to-Site VPN connection per hour**

Data transfer out on AWS Site-to-Site VPN incurs data transfer out charges that are explained in the EC2 on-demand pricing page.
[Data Transfer](https://aws.amazon.com/ec2/pricing/on-demand/)


Data Transfer OUT From Amazon EC2 To Internet	
AWS customers receive** 100GB o**f data transfer out to the internet free each month, aggregated across all
AWS Services and Regions (except China and GovCloud). The 100 GB free tier for data transfer out to the internet
is global and does not apply separately or individually to AWS Regions.	
First** 10 TB / Month	.09 per GB**

_Data Transfer OUT From Amazon EC2 To Europe (Ireland)_	**.02 per GB**

_Data Transfer within the same AWS Region_ 
Data transferred "in" to and "out" from Amazon EC2, Amazon RDS, Amazon Redshift, Amazon DynamoDB Accelerator (DAX), and Amazon ElastiCache instances, Elastic Network Interfaces or **VPC Peering connections across Availability Zones** in the same AWS Region is charged at **.01/GB** in each direction.
IPv4: Data transferred “in” to and “out” from public or Elastic IPv4 address is charged at **.01/GB **in each direction.
IPv6: Data transferred “in” to and “out” from an IPv6 address in a different VPC is charged at** .01/GB** in each direction.

Data transferred between Amazon EC2, Amazon RDS, Amazon Redshift, Amazon ElastiCache instances, and Elastic Network Interfaces in the same Availability Zone is free.


Pricing examples
Pricing example 1: Site-to-Site VPN

You create an AWS Site-to-Site VPN connection to your Amazon VPC in US East (Ohio). The connection is active for 30 days, 24 hours a day. You transfer 1,000 GB in and transfer 500 GB out through this connection.

AWS Site-to-Site VPN connection fee: There is an hourly fee for AWS Site-to-Site VPN, while connections are active. For the US East (Ohio) Region, the fee is $0.05 per hour. You pay $36.00 per month in connection fees.
Data transfer out fee: The first 100 GB are free, so you pay for 400 GB at $0.09 per GB. You pay $36.00 per month in data transfer out fees.
You pay $72.00 per month for AWS Site-to-Site VPN.

Pricing example 2: Accelerated Site-to-Site VPN

You create an Accelerated Site-to-Site VPN connection from your Amazon VPC in US East (Ohio) to a remote site in Europe. The connection is active for 30 days, 24 hours a day. You transfer 1,000 GB in and 500 GB out through that connection.

Accelerated Site-to-Site VPN connection fee: There is an hourly fee for Accelerated Site-to-Site VPN, while connections are active. For the US East (Ohio) Region, the fee is $0.05 per hour. You pay $36.00 per month in connection fees.
Data transfer out fee: The first 100 GB are free, so you are charged for 400 GB at $0.09 per GB. You pay $36.00 per month in data transfer out fees.
AWS Global Accelerator hourly fee: You pay hourly for two Global Accelerators for each hour the connection is active. The hourly fee for each Global Accelerator is $0.025, or $0.05 per hour. You pay $36.00 per month in Global Accelerator hourly fees. 
Accelerated Site-to-Site VPN Data Transfer Premium fee: The fee for VPN Data Transfer Premium is decided by the larger direction of data transfer, in this case 1,000 GB of data transferred in. The fee is $0.015 per GB for 1,000 GB of traffic between Regions in America and Europe. You pay $15.00 per month in Accelerated Site-to-Site VPN Data Transfer Premium fees.
You pay $123.00 per month for Accelerated Site-to-Site VPN.


AWS Client VPN endpoint association	$0.10 per hour
AWS Client VPN connection	$0.05 per hour



## AWS route tables
[AWS Route Table Concepts and How Route Tables Work](https://blog.claydesk.com/aws-route-table-concepts/)

[Configure route tables](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Route_Tables.html#gateway-route-table-routes)

