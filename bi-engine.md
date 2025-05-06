BI engine is in-memory service in [[GCP]] that accelerates queries in [[BigQuery]] by caching the data that is used more frequently. It improves performance without manual tuning. 

You incur costs for the reservation that you create for BI Engine capacity. The amount of data stored is constrained by the amount of capacity you purchase. To purchase BI Engine capacity, create a BI Engine reservation in the project where queries will be run.

Reserving BI. Engine capacity:
https://cloud.google.com/bigquery/docs/bi-engine-reserve-capacity#bq

variables.tf
```
variable "location" {}
variable "project" {}

variable "preferred_tables" {
  type = list(object({
    datasetId = string
    tableId   = string
  }))
}
```
resource.tf
```
locals {
  num_bytes_in_1_gb = 1073741824
}

resource "google_bigquery_bi_reservation" "reservation" {
  project  = var.project
  location = var.location
  size     = "300000"

  dynamic "preferred_tables" {
    for_each = var.preferred_tables
    content {
      project_id = var.project
      dataset_id = preferred_tables.value.datasetId
      table_id   = preferred_tables.value.tableId
    }
  }
}
```

module.tf
```
module "bi_engine_reservation" {
  source  = "path/to/resource/reservation.tf"
  project = <project>
  region  = <location>

  preferred_tables = [
    {
      datasetId = dataset_id_1,
      tableId   = table_id_1
    },
    {
      datasetId = dataset_id_2,
      tableId   = dataset_id_3
    },
	...
  ]
}
```