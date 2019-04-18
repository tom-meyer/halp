### Check a live server certificate

    openssl s_client -connect www.google.com:443

### Show certificate

    openssl x509 -in CERT -text # pem format
    openssl x509 -in CERT.der -inform der -text # der format

### Check key

    openssl rsa -in KEY -check

### Check that key/cert matches

    openssl x509 -in CERT -noout -modulus | md5sum
    openssl rsa -in KEY -noout -modulus | md5sum

### Generate an unencrypted private key

    openssl genrsa -out private.pem

### Generate self-signed cert

    openssl req -x509 -newkey rsa:4096 -keyout encrypted.pem -out cert.pem -days 365 # encrypted key is generated
    openssl rsa -in encrypted.pem -out key.pem # optionally, decrypt

### Formats: `der` vs `pem`

A `der` file has the **raw bytes** that make up the key, cert, or cert request.
A `pem` file has markers like `-----BEGIN RSA PRIVATE KEY-----`, and the
content is **base64 encoded der bytes**.

### Public parts of a key

The modulus and exponent parts of a key are not secret. Apparently, the RSA RFC
recommends 65537 (0xAQAB) to be used for the exponent, so really the unique
part of a public key is just the modulus.
