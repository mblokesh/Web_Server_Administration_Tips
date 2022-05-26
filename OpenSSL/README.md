# SAFEST WAY to check whether a certificate matches a private key, or a CSR matches a certificate on your own computer by using the OpenSSL commands below:

    openssl pkey -in privateKey.key -pubout -outform pem | sha256sum
    openssl x509 -in certificate.crt -pubkey -noout -outform pem | sha256sum
    openssl req -in CSR.csr -pubkey -noout -outform pem | sha256sum