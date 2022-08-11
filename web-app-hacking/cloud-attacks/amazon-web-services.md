# Amazon Web Services

## Aws Instance Metadata Service (IMDS)

### Overview

It’s a service that has an EC2 instance’s metadata. The metadata service stores information such as:

* `ami-id`:  An operating system id that might be googleable
* Private IP address
* Instance type: number of cores, memory, etc.
* Amazon region

The Instance Metadata Service (IMDS) can be configured to use either version 1 (IMDSv1) or version 2 ([IMDSv2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-service.html)). When IMDSv1 is used, then the metadata service **does not require authentication** and can therefore be accessed using **SSRF**. IMDS is available in the EC2 container's private network, at http://169.254.169.254.

_Note: ECS has a Task Metadata endpoint at http://169.254.170.2._&#x20;

_Note: IMDS responds to both GET and POST requests the same way, which is really useful for exploiting SSRF vulnerabilities which only allow you to do POST requests._

### Exploitation

If there’s an open HTTP proxy running on an AWS EC2 instance, then you could query the metadata service from there and get a response back.&#x20;

Let's examine an exploitation example with an open HTTP proxy. Through the proxy, you can make a request to `http://169.254.169.254/path/to/resource` and get a response back.

_Note: IMDS shows directory listings. You can start by querying `http://169.254.169.254/` to get a list of additional things you can query, and go from there._

The IMDS service contains a lot of useless stuff, for exploitation, but there are also a few gems in there.&#x20;

#### User data script

For example, you might get a `user-data` script. This is a startup script that’s written for the automation of installing and configuring the instance. The startup script might contain valuable credentials:&#x20;

* Code repositories
* Private and public keys for accessing that repo&#x20;
* API keys)

Endpoint: `http://169.254.169.254/latest/user-data`

_Note: Putting anything valuable or secret in the `user-data` script is bad practice. More commonly, secrets are in environment variables, which are loaded into the EC2 container._

#### Instance profile

Instance profiles are credentials attached to a specific EC2 instance, used to connect to other services. These are stored in the metadata service. If you can query the metadata service, then you can read the instance profile to get the creds attached to this instance.

Endpoint for getting a list of roles attached to the EC2 instance: `http://169.254.169.254/latest/meta-data/iam/security-credentials/`

Endpoint for getting the credentials of a specific role:  `http://169.254.169.254/latest/meta-data/iam/security-credentials/IAM_ROLE_HERE`

Where `IAM_ROLE_HERE` is the name of the role.

Using those creds and an [AWS pentesting tool](https://github.com/andresriancho/nimbostratus), you can test all services and see which ones you can access. Note that this is brute-forced and you might not find the full permission set. For example, the tool might miss a specific s3 bucket.

_Note: I've also seen credentials stored at_ [_http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance_](http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance)_. That was in an instance that didn't have an IAM role attached to it._

## Amazon SQS

If in the permissions list you see listQueues as access, then that’s a function in SQS API (SQS is a simple queue service for messages between software components). It means you can write and read the SQS queue.

There might be a serializer like celery in between the SQS that handles serialization and deserialization between the EC2 and the workers that consume the SQS messages. Celery for example has the pickle serializer, which is inherently insecure. And you get RCE.

If you have RCE on a machine, like a worker that uses celery, then it will also have credentials that you can dump. And its permissions may be high if it’s misconfigured. In that example, the creds were hardcoded.

## Identity and Access Management (IAM)

This section discusses problems that can emerge when IAM credentials are misconfigured.

### Creating new users

You use IAM to manage users, groups, roles, permissions, api keys. If you get a user with iam\* permissions (like misconfigured celery worker or some other thing), then you can create a user with root permissions.

### Database backup

If you have high permissions to the RDS api, then you could for example create a backup of the database (using snapshot and restore) and therefore get all the db data.

### Role reuse pivoting

I had a case where all APIs (even test apis with weak protection) had the same IAM role (which provided strong permissions). So you could easily pivot from the test env to live.

In the same environment, there was one ECR for all environments. Consequently, the prelive environment developer could upload their own images. Images were fetched and run automatically,  so uploading your own image to ECR with the correct tag would allow you to hijack the live application.

## AWS S3

### Authenticated users only

If an S3 bucket is set to be accessible by "authenticated users only", then **any** user that is authenticated to AWS can access that bucket, even complete strangers.

The AWS Extender Burpsuite plugin will cover trying out all actions which can be permitted on an S3 bucket.