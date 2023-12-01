# Availability Zones are Randomly Assigned

AWS maps accounts randomly to availability zones names.

If I put something in eu-west-1a in my account, and you do the same in your account, it's probably going to be in different physical location.

From the [docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html):

> To ensure that resources are distributed across the Availability Zones for a Region, we independently map Availability Zones to codes for each AWS account. For example, the Availability Zone us-east-1a for your AWS account might not be the same physical location as us-east-1a for another AWS account.

> To coordinate Availability Zones across accounts, you must use the AZ ID, which is a unique and consistent identifier for an Availability Zone. For example, use1-az1 is an AZ ID for the us-east-1 Region and it has the same physical location in every AWS account. You can view the AZ IDs for your account to determine the physical location of your resources relative to the resources in another account. For example, if you share a subnet in the Availability Zone with the AZ ID use1-az2 with another account, this subnet is available to that account in the Availability Zone whose AZ ID is also use1-az2.

You may also be restricted from launching new instances in a constrained AZ unless you already have an instance there, and constrained AZs may not even be available on new accounts.

