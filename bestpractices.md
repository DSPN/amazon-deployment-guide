# Best Practices

This section of the deployment guide covers recommendations for compute, storage, network and more.

## General

AWS is made up of regions which are comprised of availability zones.  We recommend deploying DSE data centers within regions.  Racks should be distributed across availability zones within that region.

### Snitches

Cassandra propagates the cluster topology using a snitch.  A number of snitches are available, including AWS specific snitches.  We do not recommend those.  Instead we recommend Gossiping Property File Snitch (GPFS) be used.  GPFS is the most widely understood snitch.  It also supports hybrid cloud scenarios.

## Compute

AWS instance types either use ephemeral instance storage or are EBS backed.

For ephemeral instance storage backed machines we recommend:
* i2.xlarge
* i2.2xlarge
* i2.4xlarge

For EBS backed machines we recommend:
* m4.large
* m4.xlarge
* m4.2xlarge
* m4.4xlarge
* c4.large
* c4.xlarge
* c4.2xlarge
* c4.4xlarge

## Storage

### Instance Storage

Traditionally DataStax has recommended SSD based instance storage for AWS deployments.  We do not recommend spinning disk (HDD) for any application.  Currently i2 machines are the only AWS instances with a viable SSD density for deploying DSE.

### EBS

EBS comes in a variety of flavors.  DSE requires lower latency storage.  For this reason we recommend EBS Provisioned IOPS or SSD (io1) for most use cases.  For analytics heavy workloads General Purpose SSD EBS (gp2) may be sufficient.

We recommend 1-2 TB of attached storage per instance.  We recommend half the allocated disk be reserved for compaction.

More information on ebs is available at http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html

## Network

### Public IP

Public IPs are the most performant method for deploying geographically distributed clusters.  This is because each IP typically has a bandwidth cap associated with it, so adding IPs scales your bandwidth cap linearly.

### VPN

Need to discuss...
http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/vpn-connections.html
