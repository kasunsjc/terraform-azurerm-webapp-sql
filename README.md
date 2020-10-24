# terraform-azurerm-webapp-sql
Create two Azure web Apps. One app for frontend and other for API. API Web App is connected to Azure SQL Database. Azure Application insight is created fro the web frontend and App insight connected to Log analytics workspace.

Following architecture will deploy for this module 

![Architecture](images/Architecture%20Diagram.png)

Example Module Deployment using variable file

```
provider "azurerm" {
  features {}
}

resource "azurerm_resource_group" "web_app_sql_rg" {
  location = var.region
  name = var.rg_name
}

module "webapp-sql" {
  source  = "kasunsjc/webapp-sql/azurerm"
  version = "1.0.0"
  app_insights = var.app_insights
  app_runtime_version = var.app_runtime_version
  app_service_plan_name = var.app_service_plan_name
  app_service_plan_size = var.app_service_plan_size
  app_service_plan_sku = var.app_service_plan_sku
  api_app_name = var.api_app_name
  log_analytics_workspace_name = var.log_analytics_workspace_name
  log_analytics_sku = var.log_analytics_sku
  sqldb_edition = var.sqldb_edition
  sql_master_password = var.sql_master_password
  sql_master_username = var.sql_master_username
  sql_svr_name = var.sql_svr_name
  sqldb_name = var.sqldb_name
  rg_name = azurerm_resource_group.web_app_sql_rg.name
  region = azurerm_resource_group.web_app_sql_rg.location
  web_app_name = var.web_app_name
}
```