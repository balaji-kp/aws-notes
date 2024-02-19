

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


