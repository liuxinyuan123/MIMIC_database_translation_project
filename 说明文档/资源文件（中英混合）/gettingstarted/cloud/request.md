---
title: "Accessing MIMIC-IV on the cloud"
linktitle: "Request"
date: 2020-11-27
weight: 2
description: >
  How to grant your linked cloud account access to MIMIC.
---

Now that your cloud credentials are available in PhysioNet, you can request access to databases within those cloud systems.
Cloud access to PhysioNet projects such as MIMIC-IV and MIMIC-III are managed independently. You must request access to the cloud systems via their project pages (access is provisioned instantly for credentialed users who have signed the DUA).

For MIMIC-III, go to the [MIMIC-III PhysioNet project page](https://physionet.org/content/mimiciii).
For MIMIC-IV, go to the [MIMIC-IV PhysioNet project page](https://physionet.org/content/mimiciv).

Once there, scroll to the bottom to the "Files" section.
*If* the page shows a restricted-access warning, you need to get access to [MIMIC](/docs/gettingstarted).
Otherwise, you should see the following:

![Methods for accessing MIMIC-IV](/img/cloud/mimiciv_files.png)

The following describes the access options listed above in the order they are listed:

1. Download the ZIP file
    * This downloads the data directly from the PhysioNet servers.
2. Request access using Google BigQuery (**Cloud**)
    * This option adds the Google e-mail in your PhysioNet account to a BigQuery access list
    * This is required in order to use the data in BigQuery.
3. Adds your AWS account ID to the access list for AWS (currently only available for MIMIC-III)(**Cloud**).
    * This is necessary in order to access the data via AWS services. For information on how to use AWS, we [recommend reading this tutorial](https://aws.amazon.com/blogs/big-data/perform-biomedical-informatics-without-a-database-using-mimic-iii-data-and-amazon-athena/).
4. Request access to the files using Google Cloud Storage Browser (only available for MIMIC-IV)(**Cloud**)
    * This option adds your Google e-mail in your PhysioNet account to the GCP access list
    * This is required in order to download the data from a storage bucket on GCP.
5. Download the files using your terminal
    * Provides a command for downloading the data from PhysioNet as individual CSV files using `wget` (when compared to the image above, your command will have a distinct username).

<!--
4. TBD. AWS is not yet available for MIMIC-IV-notNeeded.
5. TBD. AWS is not yet available for MIMIC-IV-notNeeded.

4. **Cloud**: A public page for viewing the data description in the AWS Open Data Repository.
  * This forwards you to the AWS Open Data Repository listing of the data. For information on how to use AWS, we [recommend reading this tutorial](https://aws.amazon.com/blogs/big-data/perform-biomedical-informatics-without-a-database-using-mimic-iii-data-and-amazon-athena/).
5. **Cloud**: Adds your AWS account ID to the access list for AWS.
  * This is necessary in order to access the data via AWS services. For information on how to use AWS, we [recommend reading this tutorial](https://aws.amazon.com/blogs/big-data/perform-biomedical-informatics-without-a-database-using-mimic-iii-data-and-amazon-athena/).
-->

For example, if you are interested in accessing MIMIC-IV on BigQuery, you would click "Request access using Google BigQuery". The page should provide you a green notification indicating you have been provided access.

![Access granted to Google Cloud Platform's BigQuery service](/img/cloud/bq_provisioned.png)

You will receive an e-mail detailing instructions for how to access MIMIC on BigQuery. Alternatively, instructions are also provided on the [BigQuery page](../bigquery).

## Using data on the cloud

Once you have been granted access to a cloud resource, the next step is to navigate to that resource in the cloud.

* For the GCP Storage Bucket, click the link e-mailed to you.
* For BigQuery, see the [BigQuery page](../bigquery). You may also be interested in the [querying tutorial on BigQuery] for [MIMIC-III](/docs/iii/tutorials/intro-to-mimic-iii-bq//) or [MIMIC-IV](/docs/iv/tutorials/bigquery/).
* AWS access is currently unavailable for MIMIC-IV, but planned.

Once you have access to MIMIC, we highly recommend you read the respective database introduction: [MIMIC-III](/docs/iii), [MIMIC-IV](/docs/iv/).
