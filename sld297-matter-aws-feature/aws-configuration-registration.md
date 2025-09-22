# Amazon Web Services (AWS)

Amazon Web Services offers reliable, scalable, and inexpensive cloud computing services. Refer to [AWS Documentation](https://aws.amazon.com/what-is-aws/) for more details.

## AWS CA Certificate Registration

1. Open [AWS](https://aws.amazon.com/).
2. Log in using your AWS credentials.

3. Go to **Security > Policies** and select **Create Policy**. Enter the policy name (ex: MATTER_AWS_POLICY_) and, in the policy statements, select **JSON** and replace the contents with the JSON provided below:

    ```shell
     {
       "Version": "2012-10-17",
       "Statement": [
        {
          "Effect": "Allow",
          "Action": "*",
          "Resource": "*"
        }
      ]
     }
    ```

4. Once done, select **Create**.

5. Create client CSR certificate, and a client key using the [Openssl Certificate Creation](./openssl-certificate-creation.md) documentation.

6. Steps to create a thing and generate certificates for your Matter application to use in the `MatterAwsNvmCert.cpp` source file:

    - Go to **All Devices > Things** and select **Create Things**.
    - Select **Create Single Thing** and click **Next**.
    - Specify thing properties in **Info > Give the thing a name** (Note: Client ID) and click **Next**.
    - Configure the device certificate (optional) in **Info > Upload CSR**.
    - In **Certificate > Choose file** (Choose Client CSR generated in Openssl Certificate Creation ex: `device.csr`). Click **Next**. 
    - Use the policy (ex: MATTER_AWS_POLICY_) created in AWS Certificate creation.
    - Upon successful creation, Activate the Certificate and download the certificate.

8. Copy the contents of [AWS_CA CERT](https://www.amazontrust.com/repository/AmazonRootCA3.pem) and add it as CA certificate in `MatterAwsNvmCert.cpp`. 

9. Repeat Step 5 to create a new thing to use in MQTT Explorer using the certificate created for MQTT explorer (from Openssl Certificate Creation ex: `explorer.csr`). create a .pem file from CA certificate in step 8 to use as a SERVER CERTIFICATE in MQTT Explorer.

    **Note**: Thing name must be unique as it will be used as CLIENT ID.
