---
title: Database Type Versions
layout: default
---

# Database Type Versions

--- row ---

**Database type version attributes**

{:.table}
| field            | type    | description                                                           |
| -----------      | ------- | --------------------------------                                      |
| id               | string  | unique ID identifying the database type version                       |
| database_type_id | string  | unique ID identifying the database type (e.g. PostgreSQL, MySQL, etc) |
| created_at       | date    | when the database type version was created                            |
| updated_at       | date    | when the database type version was updated                            |
| features         | array   | list of available features for this version                           |
| next_upgrade     | object  | information about the next possible upgrade (optional)                |
| allowed_plugins  | array   | array of available plugins (only for Elasticsearch)                   |
| major            | integer | major version                                                         |
| minor            | integer | minor version                                                         |
| patch            | integer | patch version                                                         |
| build            | integer | build version                                                         |

||| col |||

Example object:

```json
{
  "id": "5f217c7a406c12000e889be3",
  "created_at": "2020-07-29T15:41:14.326+02:00",
  "updated_at": "2020-07-29T15:41:14.326+02:00",
  "database_type_id": "5c9b959801dcea2f34d4969b",
  "major": 4,
  "minor": 0,
  "patch": 19,
  "build": 1,
  "features": [
    "tls"
  ],
  "next_upgrade": null,
  "allowed_plugins": null
}
```

--- row ---

## Get a Database Type Version

--- row ---

`GET https://$DB_API_URL/api/database_type_versions/[:id]`

Get a specific database type version.

||| col |||

```shell
curl -H "Accept: application/json" -H "Content-Type: application/json" \
  -H "Authorization: Bearer $DB_BEARER_TOKEN" \
  -X GET https://$DB_API_URL/api/database_type_version/5f217c7a406c12000e889be3
```

Returns 200 OK

```json
{
  "database_type_version": {
    "id": "5f217c7a406c12000e889be3",
    "created_at": "2020-07-29T15:41:14.326+02:00",
    "updated_at": "2020-07-29T15:41:14.326+02:00",
    "database_type_id": "5c9b959801dcea2f34d4969b",
    "major": 4,
    "minor": 0,
    "patch": 19,
    "build": 1,
    "features": [
      "tls"
    ],
    "next_upgrade": null,
    "allowed_plugins": null
  }
}
```
