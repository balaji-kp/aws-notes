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
