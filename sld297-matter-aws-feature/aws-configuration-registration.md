# Amazon Web Services (AWS)

Amazon Web Services offers reliable, scalable, and inexpensive cloud computing services. Refer to [AWS Documentation](https://aws.amazon.com/what-is-aws/) for more details.

## AWS CA Certificate Registration

1. Open [AWS](https://aws.amazon.com/).
2. Log in using your AWS credentials.

3. Go to **Security > Policies** and select **Create Policy**. Enter the policy name (e.g., `MATTER_AWS_POLICY_`). In the policy statements, select **JSON** and replace the contents with the JSON provided below:

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

5. Create a client CSR certificate and a client key by following the steps in the [OpenSSL Certificate Creation](./openssl-certificate-creation.md) documentation.

6. Complete the following steps to create a thing and generate certificates for your Matter application to use in the `MatterAwsNvmCert.cpp` source file:

    - Go to **All Devices > Things** and select **Create Things**.
    - Select **Create Single Thing** and click **Next**.
    - Under **Info > Give the thing a name**, specify the thing name (this will be the client ID), then click **Next**.
    - (Optional) Configure the device certificate under  **Info > Upload CSR**.
    - In **Certificate > Choose file** (Choose Client CSR generated in Openssl Certificate Creation ex: `device.csr`). Click **Next**. 
    - Use the policy (e.g., `MATTER_AWS_POLICY_`) created in AWS Certificate creation.
    - Once the thing is successfully created, activate and download the certificate.

8. Copy the contents of [AWS_CA CERT](https://www.amazontrust.com/repository/AmazonRootCA3.pem) and add it as CA certificate in `MatterAwsNvmCert.cpp`. 

9. Repeat Step 5 to create a new thing for use in MQTT Explorer, using the certificate generated for MQTT Explorer during OpenSLL certificate creation (e.g., `explorer.csr`). Create a `.pem` file from the CA certificate in step 8 and use it as the server certificate in MQTT Explorer.

    **Note**: The thing name must be unique as it will be used as the client ID.
