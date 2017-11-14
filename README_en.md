# Updating subscriber data
## Modifying multiple subscribers

endpoint: `https://emarsys.net/api/contacts/updates`

Use a modifying multiples request to modify a large number of subscribers quickly. 

One request can modify any data of any given subscriber. Use one object per subscriber to define the data to modify. Different data pieces can be modified for each subscriber.
 
If `id` key is among the data to modify, then the subscriber with that specific identifier is modified. However, subscribers are also identifiable using any other field value. In the later case, the key to use for identification must be specified in the `external_key_field` field. 

**ATTENTION**: 

When modifying multiple subscribers, **operations and timers are ignored, and no cell-sync is performed**. Use this type of data modification method *only* when you do not need these.

*IMPORTANT*: 

- When `external_key_field` is used for identification, **each object** must contain the field referenced by `external_key_field`.

- Unless the update is `id` based, **multiple subscriber records may be modified**. 
If overlooked, non-id-based updates may cause unwanted subscriber data alteration. 

### example: 
a successful update request using `external_key_field`:

#### request:

**POST** https://emarsys.net/api/contacts/updates

```json
{
    "external_key_field": "some_id_field",
    "contacts": [
        {
            "first_name": "Alma",
            "last_name": "Fa",
            "some_id_field": "qwe123"
        },
               {
            "email": "korte.fa@emarsys.com",
            "some_id_field": "asd456"
        }
    ]
}
```

#### response:

**HTTP 200**

```json
{
    "results": [
        {
            "id": 9,
            "some_field_id": "qwe123",
            "_links": {
                "href": "https://emarsys.net/api/contacts/9"
            }
        },
        {
            "id": 28,
            "some_field_id": "asd456",
            "_links": {
                "href": "https://emarsys.net/api/contacts/28"
            }
        },
        {
            "id": 41,
            "some_field_id": "asd456",
            "_links": {
                "href": "https://emarsys.net/api/contacts/41"
            }
        }
    ]
}
```
