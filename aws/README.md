Lambda Layer (python)
---------------------

    python3 -m venv venv
    source venv/bin/activate
    pip install --upgrade pip
    mkdir python
    pip install --target python -r requirements.txt
    zip -r layer-3.8.zip python


Bucket policies madness
-----------------------

There are 3 permissions systems:

- ACLs (attached to the bucket and/or object)
- Bucket policy (attached to the bucket)
- IAM policy (attached to a User or Role)

There is a good flow diagram showing how this works in the section
The best explaination of how this works is in the section "How does
authorization work with multiple access control mechanisms?" in this post:

[IAM Policies and Bucket Policies and ACLs! Oh, My!][1]

> Whenever an AWS principal issues a request to S3, the authorization decision
> depends on the union of all the IAM policies, S3 bucket policies, and S3 ACLs
> that apply.
>
> In accordance with the principle of least-privilege, decisions default to
> DENY and an explicit DENY always trumps an ALLOW. For example, if an IAM
> policy grants access to an object, the S3 bucket policies denies access to
> that object, and there is no S3 ACL, then access will be denied. Similarly,
> if no method specifies an ALLOW, then the request will be denied by default.
> Only if no method specifies a DENY and one or more methods specify an ALLOW
> will the request be allowed.

**Important note about cross-account access**

From [Restricting Access to Amazon S3 Content][2]

> If another AWS account uploads files to your bucket, that account is the
> owner of those files. Bucket policies only apply to files that the bucket
> owner owns. This means that if another account uploads files to your bucket,
> the bucket policy that you created for your OAI not evaluated for those
> files. In that case, use object ACLs to give permissions to your OAI.

However, cross-account object ownership can now be managed with a new feature:

> You can now use a new per-bucket setting to enforce uniform object ownership
> within a bucket. This will simplify many applications, and will obviate the 
> need for the Lambda-powered self-COPY that has become a popular way to do this
> up until now. Because this setting changes the behavior seen by the account
> that is uploading, the PUT request must include the `bucket-owner-full-control`
> ACL. You can also choose to use a bucket policy that requires the inclusion of
> this ACL.

Verify keypair fingerprint
--------------------------

Geez, why so complicated?

> https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#verify-key-pair-fingerprints

    openssl pkcs8 -in path_to_private_key -inform PEM -outform DER -topk8 -nocrypt | openssl sha1 -c # for key created with AWS
    openssl rsa -in path_to_private_key -pubout -outform DER | openssl md5 -c # ???
    ssh-keygen -ef path_to_private_key -m PEM | openssl rsa -RSAPublicKey_in -outform DER | openssl md5 -c # created with OpenSSH 7.8 or later and uploaded

[1]: https://aws.amazon.com/blogs/security/iam-policies-and-bucket-policies-and-acls-oh-my-controlling-access-to-s3-resources/
[2]: https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html#private-content-granting-permissions-to-oai
[3]: https://aws.amazon.com/blogs/aws/amazon-s3-update-three-new-security-access-control-features/
