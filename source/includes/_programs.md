# Programs

## Get Programs

This endpoint returns a paginated list of Programs as well as pagination links and meta information.

> GET /api/programs

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET "https://app.monami.io/api/programs?page=1&per_page=1"
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  response = Excon.get('https://app.monami.io/api/programs?page=1&per_page=1',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "programs": [
    {
      "id": 210,
      "label": "aliquid_dolores_nisi_laboriosam",
      "name": "Aliquid dolores nisi laboriosam.",
      "short_name": "animi",
      "created_at": "2024-09-06T15:56:02.173-07:00",
      "updated_at": "2024-09-06T15:56:02.173-07:00",
      "type": "internal",
      "description": null,
      "category": null,
      "reporting_framework": null,
      "external_guid": null,
      "caregiver_relationship_type": null,
      "default_funding_source_label": "label_3",
      "funding_source_labels": ["label_3", "label_4"],
      "service_definition_labels": []
    },
    {
      "id": 211,
      "label": "quas_sunt_quis_molestiae",
      "name": "Quas sunt quis molestiae.",
      "short_name": "ut",
      "created_at": "2024-09-06T15:56:02.280-07:00",
      "updated_at": "2024-09-06T15:56:02.280-07:00",
      "type": "internal",
      "description": null,
      "category": null,
      "reporting_framework": null,
      "external_guid": null,
      "caregiver_relationship_type": null,
      "default_funding_source_label": "label_5",
      "funding_source_labels": ["label_5", "label_6"],
      "service_definition_labels": []
    },
    {
      "id": 212,
      "label": "dolor_voluptatibus_similique_voluptates",
      "name": "Dolor voluptatibus similique voluptates.",
      "short_name": "voluptatem",
      "created_at": "2024-09-06T15:56:02.370-07:00",
      "updated_at": "2024-09-06T15:56:02.370-07:00",
      "type": "internal",
      "description": null,
      "category": null,
      "reporting_framework": null,
      "external_guid": null,
      "caregiver_relationship_type": null,
      "default_funding_source_label": "label_7",
      "funding_source_labels": ["label_7", "label_8"],
      "service_definition_labels": []
    }
  ],
  "links": {
    "self": "http://app.monami.test/api/programs?page=1",
    "first": "http://app.monami.test/api/programs?page=1",
    "last": "http://app.monami.test/api/programs?page=1"
  },
  "meta": {
    "total_pages": 1,
    "current_page": 1
  }
}
```

### Response Parameters

| Parameter | Description                                             |
| --------- | ------------------------------------------------------- |
| programs  | The collection of results.                              |
| links     | Pagination links to access all the pages of the results |
| meta      | Helpful response metadata                               |

### Query Parameters

| Parameter | Default | Description                 |
| --------- | ------- | --------------------------- |
| page      | 1       | Select the page of results. |
| per_page  | 25      | How many results per page.  |

<!-- <aside class="success">
Remember — the info!
</aside> -->

## Get a Specific Program

> GET /api/programs/:id

```shell
curl -i -u $MONAMI_UID:$MONAMI_SECRET https://app.monami.io/api/programs/5
```

```ruby
  credential = Base64.strict_encode64 ENV.values_at('MONAMI_UID', 'MONAMI_SECRET').join(':')

  Excon.get('https://app.monami.io/api/programs/5',
    headers: {
      'Content-Type' :  'application/json',
      'Authorization' :  "Basic #{credential}"
    }
  )
```

> A sucessful request returns JSON structured like this:

```json
{
  "id": 208,
  "label": "quia_et_iure_quidem",
  "name": "Quia et iure quidem.",
  "short_name": "repudiandae",
  "created_at": "2024-09-06T15:54:57.724-07:00",
  "updated_at": "2024-09-06T15:54:57.724-07:00",
  "type": "internal",
  "description": null,
  "category": null,
  "reporting_framework": null,
  "external_guid": null,
  "caregiver_relationship_type": null,
  "default_funding_source_label": "label_1",
  "funding_source_labels": ["label_1", "label_2"],
  "service_definition_labels": []
}
```

This endpoint retrieves a specific Program.

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->

### Program Parameters

| Parameter                    | Description                                                                                                      |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| id                           | The id of the program                                                                                            |
| name                         | The name of the program                                                                                          |
| label                        | A friendly id that can be used on APIs as well as within Mon Ami                                                 |
| short_name                   | (Optional) - An abbreviatted name for the program                                                                |
| description                  | (Optional) - A short description of this program.                                                                |
| external_guid                | (Optional) - An ID from an external system. Can also be used on supported APIs for preventing duplicate records. |
| type                         | The type of program. Ex: (internal, external, reporting_only)                                                    |
| default_funding_source_label | The label of the default funding source for this program                                                         |
| funding_source_labels        | An array of labels of the funding sources available to this program.                                             |
| service_definition_labels    | An array of labels of the service definitions associatted with this program                                      |
