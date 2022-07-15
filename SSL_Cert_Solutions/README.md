# SAFEST WAY to check whether a certificate matches a private key, or a CSR matches a certificate on your own computer by using the OpenSSL commands below:

    $ openssl pkey -in privateKey.key -pubout -outform pem | sha256sum
    $ openssl x509 -in certificate.crt -pubkey -noout -outform pem | sha256sum
    $ openssl req -in CSR.csr -pubkey -noout -outform pem | sha256sum

# Extracting Certificate and Private Key Files from a .pfx File

    1. Take the file you exported (e.g. certname.pfx) and copy it to a system where you have OpenSSL installed. Note: the *.pfx file is in PKCS#12 format and includes both the certificate and the private key.
    2. Run the following command to export the private key: openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
    3. Run the following command to export the certificate: openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
    4. Run the following command to remove the passphrase from the private key: openssl rsa -in key.pem -out server.key 

# How to Verify Password for an Encrypted SSL Certificate Key File (and remove the passphrase from private.key)

    1. SSH to the server using PuTTY, run shell, and change the directory to /ssl.
    2. View the contents of the keyfile by running cat <KeyFileName>. For example, run cat private.key
    3. At the top of the file, if you see Proc-Type: 4, ENCRYPTED, then your keyfile is encrypted (password protected).
    4. If you do not see ENCRYPTED near the top, then your keyfile is not password protected.
    5. Try decrypting the key with OpenSSL by running: openssl rsa -in MyKeyfile.key and type in the password or pass phrase.
    6. If you typed in the wrong password, then you will see unable to load Private Key.
    7. Run the following command to remove the passphrase from the private key: openssl rsa -in key.pem -out server.key 