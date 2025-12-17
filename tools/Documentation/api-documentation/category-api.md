# Category API

## Get all categories

<mark style="color:blue;">`GET`</mark> `http://lrr.tvc-16.science/api/categories`

Get all the categories saved on the server.

{% tabs %}
{% tab title="200 " %}
```javascript
[
  {
    "archives": [],
    "id": "SET_1589227137",
    "name": "doujinshi 💦💦💦",
    "pinned": "1",
    "search": "doujinshi"
  },
  {
    "archives": [],
    "id": "SET_1589291510",
    "name": "All archives by uo denim",
    "pinned": "0",
    "search": "artist:uo denim"
  },
  {
    "archives": [
      "b835f24b953c236b7bbb22414e4f2f1f4b51891a",
      "9ed04c35aa41be137e3e696d2001a2f6d9cbd38d",
      "8b0b6bb3d180eff607c941755695c317570d8449",
      "a5c0958ad25642e2204aff09f2cc8e70870bd81f",
      "32f0edeb5d5b3cf71a02b39279a69d0a903e4aed"
    ],
    "id": "SET_1589493021",
    "name": "The very best",
    "pinned": "0",
    "search": ""
  }
]
```
{% endtab %}
{% endtabs %}

## Get a single category

<mark style="color:blue;">`GET`</mark> `http://lrr.tvc-16.science/api/categories/:id`

Get the details of the specified category ID.

#### Path Parameters

| Name                                 | Type   | Description                 |
| ------------------------------------ | ------ | --------------------------- |
| id<mark style="color:red;">\*</mark> | string | ID of the Category desired. |

{% tabs %}
{% tab title="200 " %}
```
{
  "archives": [],
  "id": "SET_1613080290",
  "name": "My great category",
  "pinned": "0",
  "search": ""
}
```
{% endtab %}

{% tab title="400 " %}
```
{
  "error": "The given category does not exist.",
  "operation": "get_category",
  "success": 0
}
```
{% endtab %}
{% endtabs %}

## 🔑Create a Category

<mark style="color:orange;">`PUT`</mark> `http://lrr.tvc-16.science/api/categories`

Create a new Category.

#### Query Parameters

| Name                                   | Type    | Description                                                       |
| -------------------------------------- | ------- | ----------------------------------------------------------------- |
| pinned                                 | boolean | Add this parameter if you want the created category to be pinned. |
| search                                 | string  | Matching predicate, if creating a Dynamic Category.               |
| name<mark style="color:red;">\*</mark> | string  | Name of the Category.                                             |

{% tabs %}
{% tab title="200 " %}
```
{
  "category_id": "SET_1589383525",
  "operation": "create_category",
  "success": 1
}
```
{% endtab %}

{% tab title="400 " %}
```
{
  "error": "Category name not specified.",
  "operation": "create_category",
  "success": 0
}
```
{% endtab %}
{% endtabs %}

## 🔑Update a Category

<mark style="color:orange;">`PUT`</mark> `http://lrr.tvc-16.science/api/categories/:id`

Modify a Category.

#### Path Parameters

| Name                                 | Type   | Description                   |
| ------------------------------------ | ------ | ----------------------------- |
| id<mark style="color:red;">\*</mark> | string | ID of the Category to update. |

#### Query Parameters

| Name   | Type    | Description                                                                                                        |
| ------ | ------- | ------------------------------------------------------------------------------------------------------------------ |
| name   | string  | New name of the Category                                                                                           |
| search | string  | Predicate. Trying to add a predicate to a category that already contains Archives will give you an error.          |
| pinned | boolean | <p>Add this argument to pin the Category.</p><p>\</p><p>If you don't, the category will be unpinned on update.</p> |

{% tabs %}
{% tab title="200 " %}
```
{
  "category_id": "SET_1589573608",
  "operation": "update_category",
  "success": 1
}
```
{% endtab %}

{% tab title="400 " %}
```
{
  "error": "The given category does not exist.",
  "operation": "update_category",
  "success": 0
}
```
{% endtab %}

{% tab title="423 Locked resource" %}
```
{
  "operation": "update_category",
  "success": 0,
  "error": "Locked resource: SET_1749366470"
}
```
{% endtab %}
{% endtabs %}

## 🔑Delete a Category

<mark style="color:red;">`DELETE`</mark> `http://lrr.tvc-16.science/api/categories/:id`

Remove a Category.

#### Path Parameters

| Name                                 | Type   | Description                   |
| ------------------------------------ | ------ | ----------------------------- |
| id<mark style="color:red;">\*</mark> | string | ID of the Category to delete. |

{% tabs %}
{% tab title="200 " %}
```
{
  "operation": "delete_category",
  "success": 1
}
```
{% endtab %}

{% tab title="423 Locked resource" %}
```
{
  "operation": "delete_category",
  "success": 0,
  "error": "Locked resource: SET_1749366464"
}
```
{% endtab %}
{% endtabs %}

## 🔑Add an Archive to a Category

<mark style="color:orange;">`PUT`</mark> `http://lrr.tvc-16.science/api/categories/:id/:archive`

Adds the specified Archive ID (see Archive API) to the given Category.

#### Path Parameters

| Name                                      | Type   | Description                        |
| ----------------------------------------- | ------ | ---------------------------------- |
| id<mark style="color:red;">\*</mark>      | string | Category ID to add the Archive to. |
| archive<mark style="color:red;">\*</mark> | string | Archive ID to add.                 |

{% tabs %}
{% tab title="200 " %}
```
{
  "operation": "add_to_category",
  "success": 1,
  "successMessage": "Added \"Name of archive\" to category \"Name of category\""
}
```
{% endtab %}

{% tab title="423 Locked resource" %}
```
{
  "operation": "delete_category",
  "success": 0,
  "error": "Locked resource: SET_1749366457"
}
```
{% endtab %}
{% endtabs %}

## 🔑Remove an Archive from a Category

<mark style="color:red;">`DELETE`</mark> `http://lrr.tvc-16.science/api/categories/:id/:archive`

Remove an Archive ID from a Category.

#### Path Parameters

| Name                                      | Type   | Description |
| ----------------------------------------- | ------ | ----------- |
| id<mark style="color:red;">\*</mark>      | string | Category ID |
| archive<mark style="color:red;">\*</mark> | string | Archive ID  |

{% tabs %}
{% tab title="200 " %}
```
{
  "operation": "remove_from_category",
  "success": 1
}
```
{% endtab %}

{% tab title="423 Locked resource" %}
```
{
  "operation": "delete_category",
  "success": 0,
  "error": "Locked resource: SET_1749366450"
}
```
{% endtab %}
{% endtabs %}

## Get bookmark link

<mark style="color:blue;">`GET`</mark> `http://lrr.tvc-16.science/api/categories/bookmark_link`

Retrieves the ID of the category currently linked to the bookmark feature. Returns an empty string if no category is linked.

{% tabs %}
{% tab title="200 " %}
```
{
  "category_id": "SET_1744272066",
  "operation": "get_bookmark_link",
  "success": 1
}
```
{% endtab %}
{% endtabs %}

## 🔑Update bookmark link

<mark style="color:orange;">`PUT`</mark> `http://lrr.tvc-16.science/api/categories/bookmark_link/:id`

Links the bookmark feature to the specified static category. This determines which category archives are added to when using the bookmark button.

#### Path Parameters

| Name                                 | Type   | Description                                                  |
| ------------------------------------ | ------ | ------------------------------------------------------------ |
| id<mark style="color:red;">\*</mark> | string | ID of the static category to link with the bookmark feature. |

{% tabs %}
{% tab title="200 " %}
```
{
  "category_id": "SET_1744272066",
  "operation": "update_bookmark_link",
  "success": 1
}
```
{% endtab %}

{% tab title="400 Invalid category ID." %}
```
{
  "category_id": "SET_1744272066",
  "operation": "update_bookmark_link",
  "success": 0,
  "error": "Input category ID is invalid."
}
```
{% endtab %}

{% tab title="400 Attempted to link bookmark to a dynamic category" %}
```
{
  "category_id": "SET_1744272066",
  "operation": "update_bookmark_link",
  "success": 0,
  "error": "Cannot link bookmark to a dynamic category."
}
```
{% endtab %}

{% tab title="404 Category with specified ID does not exist" %}
```
{
  "category_id": "SET_1744272066",
  "operation": "update_bookmark_link",
  "success": 0,
  "error": "Category does not exist!"
}
```
{% endtab %}
{% endtabs %}

## 🔑Disable bookmark feature

<mark style="color:red;">`DELETE`</mark> `http://lrr.tvc-16.science/api/categories/bookmark_link`

Disables the bookmark feature by removing the link to any category. Returns the ID of the previously linked category.

{% tabs %}
{% tab title="200 " %}
```
{
  "category_id": "SET_1744272332",
  "operation": "remove_bookmark_link",
  "success": 1
}
```
{% endtab %}
{% endtabs %}
