Verify keypair fingerprint
--------------------------

Geez, why so complicated?

> https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#verify-key-pair-fingerprints

    openssl pkcs8 -in path_to_private_key -inform PEM -outform DER -topk8 -nocrypt | openssl sha1 -c # for key created with AWS
    openssl rsa -in path_to_private_key -pubout -outform DER | openssl md5 -c # ???
    ssh-keygen -ef path_to_private_key -m PEM | openssl rsa -RSAPublicKey_in -outform DER | openssl md5 -c # created with OpenSSH 7.8 or later and uploaded
