# Amazon Web Services (AWS)

Amazon Web Services offers reliable, scalable, and inexpensive cloud computing services. Refer to [AWS Documentation](https://aws.amazon.com/what-is-aws/) for more details.

## AWS CA Certitifcate Registration

1. Create a CA certificate, a CA verification certificate, a client certificate, and a client key using the [Openssl Certificate Creation](./openssl-certificate-creation.md) documentation.
2. Open [AWS](https://aws.amazon.com/).
3. Log in using your AWS credentials.
4. Register the CA Certificate in AWS:
    - Go to **Security > Certificate Authorities** and **Register CA Certificate**.
    - Select **Register CA** in the Single account mode.
    - Choose the CA certificate (CA.crt) that you previously created above.
    - Choose the CA verification certificate (verification_cert.pem) that you previously created above.
    - Register the CA.

5. Go to **Security > Policies** and select **Create Policy**. Enter the policy name (ex: _DIC_POLICY_) and, in the policy statements, select **JSON** and replace the contents with the JSON provided below:

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

6. Once done, select **Create**.

7. Steps to generate the certificate for your Matter application to use in the `dic_nvm_cert.cpp` source file:

    - Go to **All Devices > Things** and select **Create Things**.
    - Select **Create Single Thing** and click **Next**.
    - Specify thing properties in **Info > Give the thing a name** (Note: Client ID) and click **Next**.
    - Configure the device certificate (optional) in **Info > Use my certificate**.
    - In Certificate details, choose **CA is registered with AWS IOT** and select the CA registered with AWS in Step 4.
    - In **Certificate > Choose file** (Choose Client certificate generated in Openssl Certificate Creation ex: `device.crt`), set the certificate status to **Active**. Click **Next**.
    - Use the policy (ex: _DIC_POLICY_) created in AWS Certificate creation.

8. Repeat Step 5 to create a new thing to use in MQTT Explorer using the certificate created for MQTT explorer (from Openssl Certificate Creation ex: `explorer.crt`).

    **Note**: Thing name must be unique as it will be used as CLIENT ID.
  
9. Copy the contents of [AWS_CA CERT](https://www.amazontrust.com/repository/AmazonRootCA1.pem) and create a .pem file to use as a SERVER CERTIFICATE in MQTT Explorer.

## How to Create AWS OTA JOB

1. Go to AWS Amazon: https://aws.amazon.com/.
2. Log in with Amazon Credentials.
3. Click **Services** and select **IOT Core**.
4. On the side menu in the **Manage** section, click **Remote Actions** and click **jobs**.
5. Click **Create Job** and select Job type as a Create FreeRTOS OTA update job.
6. Enter a unique Job name without spaces.
7. In the **Devices to update** dropdown, select your Certificates which are configured above. for example:- SQA_DIC_C2, SQA_DIC_C3, DIC_2
8. Select **MQTT** as the protocol for file transfer.
9. In **File Section**, select **New/Previously/Custom** signed **gbl(For EFR32)** and **.rps(For 917 SOC)** file.

    - If the **gbl or rps** file is newly created, then select **Sign a new file for me**.
    - If the **gbl or rps** file is already uploaded to AWS, then select **Choose a previously signed file**.
    - If the **gbl or rps** file is custom modified, then select **Use my custom signed file**.

10. In **Existing code signing profile**, select **dic_ota_codesign**. Refer to [AWS Code Signing Certificate Creation](https://docs.aws.amazon.com/freertos/latest/userguide/ota-code-sign-cert.html).
11. For uploading the **gbl or rps** file, follow step 9 above. To create a **gbl** refer to [Matter OTA](/matter/{build-docspace-version}/matter-ota) and for **rps** file, refer to [Matter OTA Software Update](/matter/{build-docspace-version}/matter-ota/04-ota-software-update-soc).
12. In the File upload location in S3 select, S3 URL as ota_demo. Refer to [AWS S3 Bucket Creation](https://docs.aws.amazon.com/freertos/latest/userguide/dg-ota-bucket.html).
13. In **Path name of file on device**, give any file name (file.txt).
14. Select **ota_demo** as **IAM role** and click **Next**.
15. Click **create job**.

Note: For more details, Refer to [AWS OTA prerequisites](https://docs.aws.amazon.com/freertos/latest/userguide/ota-prereqs.html).
