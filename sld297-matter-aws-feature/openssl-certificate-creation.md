# OpenSSL Certificate Creation

An SSL certificate is an important way to secure user information and protect against hackers.

## Openssl Installation (In ubuntu 22.04)

1. To install openssl (v 3.0.2) - `sudo apt install openssl`

## Certificates Creation

The following commands are used to generate certificates:

1. To generate Client key:
    - `openssl ecparam -name prime256v1 -genkey -noout -out device.key`
2. To generate Client certificate (ex: `device.crt` and `device.key`) using CA
   certficate:
    - `openssl req -new -out device.csr -key device.key`
3. While creating AWS thing , use Upload CSR option in configure device
   certificate step. once uploaded the CSR generated in step 2. AWS will
   generate AWS CA authenticated device.crt.
   ![AWS CSR Upload ](./images/matter_aws_device_csr_certificate_generation.png)

Repeat step 1 and 2 to create an additional set of certificate to use in MQTT
explorer (ex: `explorer.crt` and `explorer.key`). (Create with different name
for Identification)
