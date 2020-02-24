---
layout: post
title: How to create a ca and certs
comments: true
---

Here is a snippet that can be used to create a CA and certificates for apps.

    # create CA
    openssl genrsa -out ca.key 4096
    # Generate self-signed Root certificate
    openssl req -new -x509 -key ca.key -sha256 -subj "/C=IE/ST=IE/O=Cazzimia Inc." -days 365 -out ca.cert
    # Create a Key certificate for the Server
    openssl genrsa -out service.key 4096
    # Create a signing CSR
    openssl req -new -key service.key -out service.csr
    # Generate a certificate for the Server
    openssl x509 -req -in service.csr -CA ca.cert -CAkey ca.key -CAcreateserial -out service.pem -days 365 -sha256 -extensions req_ext
    # Verify cert
    openssl x509 -in service.pem -text -noout

This has been useful lately as of late
