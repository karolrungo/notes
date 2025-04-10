BI engine is in-memory service in [[GCP]] that accelerates queries in [[BigQuery]] by caching the data that is used more frequently. It improves performance without manual tuning. 

You incur costs for the reservation that you create for BI Engine capacity. The amount of data stored is constrained by the amount of capacity you purchase. To purchase BI Engine capacity, create a BI Engine reservation in the project where queries will be run.

Reserving BI. Engine capacity:
https://cloud.google.com/bigquery/docs/bi-engine-reserve-capacity#bq

Terraform:
```
resource "google_bigquery_bi_reservation" "reservation" {
    location   = "us-west2"
    size   = "3000000000"
}
```
TODO dynamic preferedTables