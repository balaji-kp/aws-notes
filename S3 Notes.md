###s3
bucket and object
data consistency model 
	read-after wirte consistency for PUT new obejct
	evently consistency for PUT or Delete new object

For example, if you PUT to an existing key, a subsequent read might
return the old data or the updated data, but it will never write corrupted or partial data.

reduced redency storage - 99.99% durability, recomandation to store non production data

bucket policy - centralized access controle to bucket and object based on varies conditions
	requester(principle), resource, action
	the permission attached to bucket apply to all object  in that bucket
Using Iam with s3 we can manage access to bucket and object for IAM user or group
 
paying for S3
	
stroage class
standard - 9's durablity
rrs
glacier
pre-signed url
lifecycele management
static web hosting
versioning	
access management
	resource based and user based access policy
	bucket policy		IAM policy on user
	ACL
	(use ACLs to grant basic read/write permissions to other AWS
accounts)
Cors - support to configure you bucket allow cross orgin request
logging - save bucket access logs.
All resouce are private, only resouce owner can access

access policy element:
	resouces
	action
	effect
	principal
data encryption
	client side
	server side 	(ASE 256)
presigned URL

Managing Access Permissions to
Your Amazon S3 Resources
By default, all Amazon S3 resources—buckets, objects, and related subresources (for example, lifecycle
configuration and website configuration)—are private: only the resource owner, an AWS account that
created it, can access the resource. The resource owner can optionally grant access permissions to
others by writing an access policy.
Amazon S3 offers access policy options broadly categorized as resource-based policies and user policies.
Access policies you attach to your resources (buckets and objects) are referred to as resource-based
policies. For example, bucket policies and access control lists (ACLs) are resource-based policies.You
can also attach access policies to users in your account.These are called user policies.You may choose
to use resource-based policies, user policies, or some combination of these to manage permissions to
your Amazon S3 resources

By default, all Amazon S3 resources are private. Only a resource owner can access the resource. The
resource owner refers to the AWS account that creates the resource. For example:
• The AWS account that you use to create buckets and objects owns those resources.
• If you create an AWS Identity and Access Management (IAM) user in your AWS account, your AWS
account is the parent owner. If the IAM user uploads an object, the parent account, to which the user
belongs, owns the object.
• A bucket owner can grant cross-account permissions to another AWS account (or users in another
account) to upload objects. In this case, the AWS account that uploads objects owns those objects.
The bucket owner does not have permissions on the objects that other accounts own, with the following
exceptions:
• The bucket owner pays the bills. The bucket owner can deny access to any objects, or delete any
objects in the bucket, regardless of who owns them.

For example, if you configure your bucket as
a website, you may want to make objects public by granting the GET Object permission to everyone.

The following is an example bucket policy.You express bucket policy (and user policy) using a JSON
file. The policy grants anonymous read permission on all objects in a bucket. The bucket policy has
one statement, which allows the s3:GetObject action (read permission) on objects in a bucket
named examplebucket. By specifying the principal with a wild card (*), the policy grants anonymous access
{
 "Version":"2012-10-17",
 "Statement":[{
 "Effect":"Allow",
 "Principal": "*",
 "Action":["s3:GetObject"],
 "Resource":["arn:aws:s3:::examplebucket/*"
 ]
 }
 ]
}

The following is an example of a user policy.You cannot grant anonymous permissions in an IAM user
policy, because the policy is attached to a user. The example policy allows the associated user that
it's attached to perform six different Amazon S3 actions on a bucket and the objects in it.You can attach
this policy to a specific IAM user, group, or role.
{
 "Statement":[
 {
 "Effect":"Allow",
 "Action":[
 "s3:PutObject",
 "s3:GetObject",
 "s3:DeleteObject",
 "s3:ListAllMyBuckets",
 "s3:GetBucketLocation",
 "s3:ListBucket"
 ],
 "Resource":"arn:aws:s3:::examplebucket/*"
 }
 ]
}
When Amazon S3 receives a request—for example, a bucket or an object operation—it first verifies that
the requester has the necessary permissions. Amazon S3 evaluates all the relevant access policies, user
policies, and resource-based policies (bucket policy, bucket ACL, object ACL) in deciding whether to
authorize the request. The following are some of the example scenarios:
• If the requester is an IAM user, Amazon S3 must determine if the parent AWS account to which the
user belongs has granted the user necessary permission to perform the operation. In addition, if the
request is for a bucket operation, such as a request to list the bucket content, Amazon S3 must verify
that the bucket owner has granted permission for the requester to perform the operation.
Note
To perform a specific operation on a resource, an IAM user needs permission from both the
parent AWS account to which it belongs and the AWS account that owns the resource.

When to Use a User Policy
In general, you can use either a user policy or a bucket policy to manage permissions.You may choose
to manage permissions by creating users and managing permissions individually by attaching policies to
users (or user groups), or you may find that resource-based policies, such as a bucket policy, work better
for your scenario.
Note that AWS Identity and Access Management (IAM) enables you to create multiple users within your
AWS account and manage their permissions via user policies. An IAM user must have permissions from
the parent account to which it belongs, and from the AWS account that owns the resource the user wants
to access. The permissions can be granted as follows:
• Permission from the parent account – The parent account can grant permissions to its user by attaching a user policy.
• Permission from the resource owner – The resource owner can grant permission to either the IAM
user (using a bucket policy) or the parent account (using a bucket policy, bucket ACL, or object ACL).

When to Use a Bucket Policy
If an AWS account that owns a bucket wants to grant permission to users in its account, it can use either
a bucket policy or a user policy. But in the following scenarios, you will need to use a bucket policy.
• You want to manage cross-account permissions for all Amazon S3 permissions – You can use
ACLs to grant cross-account permissions to other accounts, but ACLs support only a finite set of permission (What Permissions Can I Grant? (p. 358)), these don't include all Amazon S3 permissions. For
example, you cannot grant permissions on bucket subresources (see Managing Access Permissions
to Your Amazon S3 Resources (p. 263)) using an ACL.
Although both bucket and user policies support granting permission for all Amazon S3 operations (see
Specifying Permissions in a Policy (p. 308)), the user policies are for managing permissions for users
in your account. For cross-account permissions to other AWS accounts or users in another account,
you must use a bucket policy.

Bucket Owner Granting Its Users Bucket Permissions

In the Principal statement, Dave is identified by his user ARN. For more information about
policy elements, see Access Policy Language Overview (p. 305).
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Sid": "statement1",
 "Effect": "Allow",
 "Principal": {
 "AWS": "arn:aws:iam::AccountA-ID:user/Dave"
 },
 "Action": [
 "s3:GetBucketLocation",
 "s3:ListBucket"
 ],
 "Resource": [
 "arn:aws:s3:::examplebucket"
 ]
 },
 {
 "Sid": "statement2",
 "Effect": "Allow",
 "Principal": {
 "AWS": "arn:aws:iam::AccountA-ID:user/Dave"
 },
 "Action": [
 "s3:GetObject"
 ],
 "Resource": [
 "arn:aws:s3:::examplebucket/*"
 ]
 }
 ]
}
user based policy:

b. Attach the following user policy to user Dave. The policy grants Dave the s3:PutObject permission.You need to update the policy by providing your bucket name.
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Sid": "PermissionForObjectOperations",
 "Effect": "Allow",
 "Action": [
 "s3:PutObject"
 ],
 "Resource": [
  "arn:aws:s3:::examplebucket/*"
 ]
 }
 ]
}

Testing the permission via cli

creating user profile with IAM user secret key and access key:
[profile UserDaveAccountA]
aws_access_key_id = access-key
aws_secret_access_key = secret-access-key
region = us-east-1

following command to put object 
```
aws s3api put-object --bucket examplebucket --key HappyFace.jpg --body 
HappyFace.jpg --profile UserDaveAccountA
```

following command to get object:
```
aws s3api get-object --bucket examplebucket --key HappyFace.jpg OutputFile.jpg
 --profile UserDaveAccountA

```

Bucket Owner Granting Cross-Account Bucket
Permissions

An AWS account—for example, Account A—can grant another AWS account, Account B, permission to
access its resources such as buckets and objects. Account B can then delegate those permissions to
users in its account. In this example scenario, a bucket owner grants cross-account permission to another
account to perform specific bucket operations.

Attach the following bucket policy to examplebucket. The policy grants Account B permission for
the s3:GetBucketLocation and s3:ListBucket actions.
For instructions on editing bucket permissions, go to Editing Bucket Permissions in the Amazon
Simple Storage Service Console User Guide. Follow these steps to add a bucket policy.
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Sid": "Example permissions",
 "Effect": "Allow",
 "Principal": {
 "AWS": "arn:aws:iam::AccountB-ID:root"
 },
 "Action": [
 "s3:GetBucketLocation",
 "s3:ListBucket"
 ],
 "Resource": [
 "arn:aws:s3:::examplebucket"
 ]
 }
 ]
}

Verify Account B (and thus its administrator user) can perform the operations.
• Using the AWS CLI
aws s3 ls s3://examplebucket --profile AccountBadmin
aws s3api get-bucket-location --bucket examplebucket --profile AccountBadmin

Step 2.2: Create User Dave in Account B
1. In the IAM console, create a user, Dave.
For instructions, go to Adding an IAM User (AWS Management Console) in Using IAM.
2. Note down the UserDave credentials.
Step 2.3: Delegate Permissions to User Dave
• Attach the following user policy to user Dave.You will need to update the policy by providing your
bucket name.
It is assumed you are signed in to the console using AccountBadmin user credentials.
{
 "Version": "2012-10-17",
 "Statement": [
 {
 "Sid": "Example",
 "Effect": "Allow",
 "Action": [
 "s3:ListBucket"
 ],
 "Resource": [
 "arn:aws:s3:::examplebucket"
 ]
 }
 ]
}

