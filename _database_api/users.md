---
title: Users
layout: default
---

# Users

--- row ---

**User attributes**

{:.table}
| field       | type    | description                      |
| ----------- | ------- | -------------------------------- |
| name        | string  | name of the user                 |
| read_only   | boolean | true if the user is read only    |

||| col |||

Example object:

```json
{
  "name": "metabase",
  "read_only": true
}
```

--- row ---

## List Database Users

--- row ---

`GET https://db-api.scalingo.com/api/databases/[:db]/users`

List all users for a database.

||| col |||

```shell
curl -H "Accept: application/json" -H "Content-Type: application/json" \
  -H "Authorization: Bearer $DB_BEARER_TOKEN" \
  -X GET https://db-api.scalingo.com/api/databases/my-db-123/users
```

Returns 200 OK

```json
{
  "database-users": [
    {
      "name": "my-db-123",
      "read_only": false
    },
    {
      "name": "metabase",
      "read_only": true
    }
  ]
}

```

--- row ---

## Create a New Backup

--- row ---

`POST https://db-api.scalingo.com/api/databases/[:db]/backups`

Schedule the creation of a new backup. This query is asynchronous. The HTTP
query returns 201 and the backup creation is actually started asynchronously.

||| col |||

```shell
curl -H "Accept: application/json" -H "Content-Type: application/json" \
  -H "Authorization: Bearer $DB_BEARER_TOKEN" \
  -X POST https://db-api.scalingo.com/api/databases/my-db-123/backups
```

Returns 201 Created

```json
{
  "id": "5b8b36104ffb090be1ac3ce1",
  "created_at": "2019-07-18T03:00:00.178+02:00",
  "name": "20180902010000_kibana-3938",
  "size": 0,
  "status": "pending",
  "database_id": "597601234ffb097af4f3099b",
  "type": "postgresql"
}

```

--- row ---
## Get a Backup Download Link

--- row ---

`GET https://db-api.scalingo.com/api/databases/[:db]/backups/[:backup]/archive`

Get a pre-signed URL to download your backup

||| col |||

```shell
curl -H "Accept: application/json" -H "Content-Type: application/json" \
  -H "Authorization: Bearer $DB_BEARER_TOKEN" \
  -X GET https://db-api.scalingo.com/api/databases/my-db-123/backups/abcdefabcdefabcdef/archive
```

Returns 200 OK

```json
{
  "download_url": "https://db-api.scalingo.com/api/databases/my-db-123/backups/5b8a36104ffb090be1ac3ce1/download?token=token1234"
}
```
