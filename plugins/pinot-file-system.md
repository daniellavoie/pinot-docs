# Pinot File System

File System is a set of plugins devoted to storage purpose.

Currently supported file systems are:

* ADLS \(Azure Data Lake Storage\)
* GCS \(Google Cloud Storage\)

  * To configure the GcsPinotFS filesystem, the server and controller must be configured as shown below. The account associated with the `GCP_KEY_FILE` must be able to create and drop objects in the gcs bucket, for example if the account has the `Storage Admin` and `Storage Object Admin` roles for the bucket that will be sufficient. The data directory on the controller will point to gcs.
  * Jvm options should include the gcs plugin:

  ```text
  -Dplugins.dir=/opt/pinot/plugins -Dplugins.include=pinot-gcs
  ```

   

  * Controller config:

  ```text
  controller.data.dir=gs://<bucket>/<directory>/
  pinot.controller.storage.factory.class.gs=org.apache.pinot.plugin.filesystem.GcsPinotFS
  pinot.controller.storage.factory.gs.projectId=<project id>
  pinot.controller.storage.factory.gs.gcpKey=<location of gcp json key>
  pinot.controller.segment.fetcher.protocols=file,http,gs
  pinot.controller.segment.fetcher.gs.class=org.apache.pinot.common.utils.fetcher.PinotFSSegmentFetcher 
  ```

  * Server config:

  ```text
  pinot.server.storage.factory.class.gs=org.apache.pinot.plugin.filesystem.GcsPinotFS
  pinot.server.storage.factory.gs.projectId=<project id>
  pinot.server.storage.factory.gs.gcpKey=<location of gcp json key>
  pinot.server.segment.fetcher.protocols=file,http,gs
  pinot.server.segment.fetcher.gs.class=org.apache.pinot.common.utils.fetcher.PinotFSSegmentFetcher    
  ```

   

* HDFS
* S3

  * To configure the S3PinotFS filesystem, the server and controller must be configured as shown below. The account associated with the provided AWS credentials must be able to create and drop objects in the S3 bucket, for example if the account has the `Storage Admin` and `Storage Object Admin` roles for the bucket that will be sufficient. The data directory on the controller will point to S3.
  * Jvm options should include the S3 plugin:
  * ```
    -Dplugins.dir=/opt/pinot/plugins -Dplugins.include=pinot-s3
    ```
  * Controller config:

    ```text
    controller.data.dir=s3://<bucket>/<directory>/
    pinot.controller.storage.factory.class.s3=org.apache.pinot.plugin.filesystem.S3PinotFS
    pinot.controller.storage.factory.s3.region=<s3-bucket-region>
    pinot.controller.storage.factory.s3.accessKey=<aws-access-key>
    pinot.controller.storage.factory.s3.secretKey=<aws-secret-key>
    pinot.controller.segment.fetcher.protocols=file,http,s3
    pinot.controller.segment.fetcher.s3.class=org.apache.pinot.common.utils.fetcher.PinotFSSegmentFetcher 
    ```

  * Server config:

  ```text
  pinot.server.storage.factory.class.s3=org.apache.pinot.plugin.filesystem.S3PinotFS
  pinot.server.storage.factory.s3.region=<s3-bucket-region>
  pinot.server.storage.factory.s3.accessKey=<aws-access-key>
  pinot.server.storage.factory.s3.secretKey=<aws-secret-key>
  pinot.server.segment.fetcher.protocols=file,http,s3
  pinot.server.segment.fetcher.s3.class=org.apache.pinot.common.utils.fetcher.PinotFSSegmentFetcher    
  ```

You can also provide the Access Key and Secret key by setting the Environment Variables - **AWS\_ACCESS\_KEY\_ID** and **AWS\_SECRET\_ACCESS\_KEY**.

You can also use java options: **-Daws.accessKeyId** and **-Daws.secretKey** for providing AWS credentials

