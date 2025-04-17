---
title: "BigQuery"
linktitle: "BigQuery"
date: 2020-08-10
weight: 3
description: >
  Access MIMIC IV on BigQuery.
---

BigQuery is a columnar, distributed relational database management system. BigQuery accesses only the columns specified in the query, making it ideal for data analysis workflows. [Read more about BigQuery in Google's cloud documentation](https://cloud.google.com/bigquery/).

First, ensure you have been provisioned access to MIMIC III or IV on BigQuery. See the [cloud page for instructions](../../cloud). Once you have been provisioned access to using MIMIC on BigQuery, it's worthwhile to "pin" the dataset to see it on the BigQuery web tool.

1. Go to the BigQuery console: http://console.cloud.google.com/bigquery
2. If you haven’t created a BigQuery project previously you will be asked to do so. You will need to enter information to pay for the cost of queries. For more details see: https://cloud.google.com/resource-manager/docs/creating-managing-projects
3. On the left sidebar, next to "Explorer", click "+ ADD DATA". Click "Star a project by name".
4. Type `physionet-data` and enter it in.
5. In the sidebar on the left, you should now see the `physionet-data` project. Click the arrow to the left of `physionet-data` to expand the project.
6. You should now see a number of datasets. Which datasets you see depends on the access provisioned to you.
  * At a minimum, you will see the demo projects: `eicu_crd_demo` and `mimiciii_demo`.
  * If you have successfully requested access to MIMIC-III, you will additionally see `mimiciii_clinical`, `mimiciii_demo`, `mimiciii_notes`, and `mimiciii_derived`.
  * If you have successfully requested access to MIMIC-IV, you will additionally see `mimiciv_icu` and `mimiciv_hosp`.
  * If you have successfully requested access to MIMIC-IV-ED, you will additionally see `mimiciv_ed`.
  * If you have successfully requested access to MIMIC-IV-Note, you will additionally see `mimiciv_note`.
  
You are now ready to query the data! Try a simple query in the main dialogue box, while logged in under your project that pays for queries.

```sql
SELECT *
FROM `physionet-data.mimiciv_hosp.patients`
WHERE subject_id < 10000100
ORDER BY subject_id
```

The query should return some data, and your browser window should be similar to the below:

![Example output for the query](/img/cloud/bq/example_query.png)

At this point you are ready to use MIMIC on BigQuery!

A tutorial on using BigQuery to query MIMIC-III is available [here](/docs/iii/tutorials/intro-to-mimic-iii-bq).

Note that we have a number of pre-generated "views" of the data. These are available in the `mimiciv_derived` dataset which you are free to query. All code used to generate these views has been made openly available on the [MIMIC-IV code repository](https://github.com/MIT-LCP/mimic-iv/).

If you are having issues, see the [Troubleshooting section](#troubleshooting).

## Troubleshooting

### I get a pop-up about Terms of Service

![Agree to the terms of service](/img/cloud/bq/agree_tos.png)

You will need to agree to all GCP Terms of Service and adhere to their terms in order to use the data on BigQuery.

### When I go to BigQuery, it asks me to create a project

![Create a project on GCP](/img/cloud/bq/create_project.png)

Almost all of your interactions with GCP are associated with a *project*. Importantly, all billing for your usage must be allotted to a single project.
In order to use BigQuery you must have an activate project associated with your account. BigQuery offers a $300 free trial for first time users.

Create a project and select it as your activate project. If you've done this correctly, then the top bar of the Google console page should stop saying "Select a project", and instead have your project name. For example, in the below, I have selected the project `alistairewj`, which is now the activate project:

![Example of a working activate project](/img/cloud/bq/active_project.png)


### I can only see `eicu_crd_demo` and `mimiciii_demo`

These datasets are fully public, so the implication is that you have not been granted access to the full versions of the databases.
Please (1) double check you have entered your cloud information into your PhysioNet profile, verifying any e-mails as needed, and (2) requested access to the specific cloud project on its respective PhysioNet project page.

### I want to ask a question about MIMIC or raise an issue on the MIMIC Code Repository

If none of the above have the answer, feel free to [raise an issue](https://github.com/MIT-LCP/mimic-code/issues) or [ask for advice](https://github.com/MIT-LCP/mimic-code/discussions) in the MIMIC repository.
