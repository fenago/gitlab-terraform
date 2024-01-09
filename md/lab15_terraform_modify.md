
# Lab 15: Modifying the Terraform script to update the CockroachDB deployment

This lab shows you how to modify the Terraform script to update the CockroachDB deployment
using the CockroachDB Cloud Terraform provider.


## Before you begin

Before you start this lab, make sure you have created the cluster in Lab 6.


## Update the Terraform configuration files

Terraform uses a infrastructure-as-code approach to managing resources.
Terraform configuration files allow you to define resources
declaratively and let Terraform manage their lifecycle.


In this lab, you will update a CockroachDB Serverless cluster.

2.  In a text editor, update the `terraform.tfvars` file created ion lab3 with the following settings:

    
    ```
    cluster_name = "{cluster name}"
    sql_user_name = "{SQL user name}"
    sql_user_password = "{SQL user password}"
    ```
    

    Where:

    -   `{cluster name}` is the name of the cluster you want to create.
    -   `{SQL user name}` is the name of the SQL user you want to
        create.
    -   `{SQL user password}` is the password for the SQL user you want
        to create.

    For example, the following `terraform.tfvars` file creates a
    CockroachDB Serverless with a `maxroach2` SQL user.

    
    ```
    cluster_name = "blue-dog"
    sql_user_name = "maxroach2"
    sql_user_password = "Fenago@12345"
    ```
    

3.  Create an environment variable named `COCKROACH_API_KEY`. Copy the `API key` created in Lab 6.

    
    ```
    export COCKROACH_API_KEY={API key}
    ```
    

    Where `{API key}` is the API key you copied from the CockroachDB Cloud Console.



## Update the cluster


2.  Create the Terraform plan. This shows the actions the provider will
    take, but won\'t perform them:

    
    ```
    terraform plan
    ```
    

3.  Update the cluster:

    
    ```
    terraform apply
    ```
    

    Enter `yes` when prompted to apply the plan and uodate the cluster.


## Get information about your cluster

The `terraform show` command shows detailed information of your cluster
resources.


```
terraform show
```


This will show the following output:


```
# cockroach_cluster.example:
resource "cockroach_cluster" "example" {
    cloud_provider    = "GCP"
    cockroach_version = "v23.1"
    creator_id        = "a907013c-a5e2-40fc-b120-775bf0a9289e"
    id                = "60f9e362-ee83-4cbd-ab14-10535797e06d"
    name              = "blue-dog"
    operation_status  = "UNSPECIFIED"
    plan              = "SERVERLESS"
    regions           = [
        {
            internal_dns = ""
            name         = "us-central1"
            node_count   = 0
            primary      = true
            sql_dns      = "blue-dog-13786.5xj.gcp-us-central1.cockroachlabs.cloud"
            ui_dns       = ""
        },
    ]
    serverless        = {
        routing_id  = "blue-dog-13786"
        spend_limit = 0
    }
    state             = "CREATED"
    upgrade_status    = "FINALIZED"
}

# cockroach_database.example:
resource "cockroach_database" "example" {
    cluster_id  = "60f9e362-ee83-4cbd-ab14-10535797e06d"
    id          = "60f9e362-ee83-4cbd-ab14-10535797e06d:example-database"
    name        = "example-database"
    table_count = 0
}

# cockroach_sql_user.example:
resource "cockroach_sql_user" "example" {
    cluster_id = "60f9e362-ee83-4cbd-ab14-10535797e06d"
    id         = "60f9e362-ee83-4cbd-ab14-10535797e06d:maxroach2"
    name       = "maxroach2"
    password   = (sensitive value)
}
```



**Note:** You can delete the cluster by running `terraform destroy` command but you will be using cluster in upcoming labs so **don't** delete it yet.



### Task: Update the Cluster Name

Update **cluster_name** in `terraform.tfvars` and run the above terraform commands. You will get an error.

```
root@763b492af032:~/Desktop# terraform apply
cockroach_cluster.example: Refreshing state... [id=60f9e362-ee83-4cbd-ab14-10535797e06d]
\u2577
\u2502 Error: Cannot update cluster name
\u2502 
\u2502   with cockroach_cluster.example,
\u2502   on main.tf line 51, in resource "cockroach_cluster" "example":
\u2502   51: resource "cockroach_cluster" "example" {
\u2502 
\u2502 To prevent accidental deletion of data, renaming clusters isn't allowed.
\u2502 Please explicitly destroy this cluster before changing its name.
\u2575
```

