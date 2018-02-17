### Check a live server certificate

    openssl s_client -connect www.google.com:443

### Show certificate

    openssl x509 -in CERT -text

### Check key

    openssl rsa -in KEY -check

### Check that key/cert matches

    openssl x509 -in CERT -noout -modulus | md5sum
    openssl rsa -in KEY -noout -modulus | md5sum

### Generate self-signed cert

    openssl req -x509 -newkey rsa:4096 -keyout enc_key.pem -out cert.pem -days 365 # encrypted key is generated
    openssl rsa -in enc_key.pem -out key.key # optionally, decrypt
