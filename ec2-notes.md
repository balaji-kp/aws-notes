

Instance Family Current Generation Instance Types
General purpose t2.micro | t2.small | t2.medium | m3.medium | m3.large |
m3.xlarge | m3.2xlarge
Compute optimized c3.large | c3.xlarge | c3.2xlarge | c3.4xlarge | c3.8xlarge
Memory optimized r3.large | r3.xlarge | r3.2xlarge | r3.4xlarge | r3.8xlarge
Storage optimized  i2.xlarge | i2.2xlarge | i2.4xlarge | i2.8xlarge |
hs1.8xlarge
GPU instances g2.2xlarge

What is a CPU credit?
One CPU credit is equal to one vCPU running at 100% utilization for one minute. Other combinations of
vCPUs, utilization, and time are also equal one CPU credit, such as one vCPU running at 50% utilization
for two minutes, or two vCPUs (on t2.medium instances, for example) running at 25% utilization for two
minutes.

###Placement Groups
A placement group is a logical grouping of instances within a single Availability Zone. Using placement
groups enables applications to participate in a low-latency, 10 Gbps network. Placement groups are recommended for applications that benefit from low network latency, high network throughput, or both. To
provide the lowest latency, and the highest packet-per-second network performance for your placement
group, choose an instance type that supports enhanced networking.
We recommend that you launch the number of instances that you need in the placement group in a single
launch request and that you use the same instance type for all instances in the placement group.

If the root device for your instance is an Amazon EBS volume, you can easily resize your instance by
changing its instance type.
• If the root device for your instance is an instance store volume, you must migrate to a new instance.

Spot Instances
If you have flexibility on when your application will run, you can bid on unused Amazon EC2 compute
capacity, called Spot Instances, and lower your costs significantly. Set by Amazon EC2 based on the last
fulfilled bid price, the Spot Price for these instances fluctuates periodically depending on the supply of
and demand for Spot Instance capacity.
To use Spot Instances, you place a Spot Instance request (your bid) specifying the maximum price you
are willing to pay per hour per instance. If the maximum price of your bid is greater than the current Spot
Price, your request is fulfilled and your instances run until you terminate them or the Spot Price increases
above your maximum price.Your instance can also be terminated when your bid price equals the market
price, even when there is no increase in the market price. This can happen when demand for capacity
rises, or when supply fluctuates.

auto scalling group with spot instance


