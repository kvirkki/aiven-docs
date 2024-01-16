---
title: avn service tags
---

Here you\'ll find the full list of commands for `avn service tags`.

## Manage service tags

### `avn service tags list`

Retrieves the tags associated with an Aiven service.

<table>
  <thead>
    <tr><th>Parameter</th><th>Information</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>`service_name`</td>
      <td>The name of the service</td>
    </tr>
  </tbody>
</table>


**Example:** Retrieve the tags associated with the service named
`kafka-demo`.

``` 
avn service tags list kafka-demo
```

``` text
KEY      VALUE
=======  ===================
team     frontend
scope    userclicks-tracking
```

**Example:** Retrieve the tags associated with the service named
`kafka-demo` in JSON format.

``` 
avn service tags list kafka-demo --json
```

``` json
[
    {
        "key": "team",
        "value": "frontend"
    },
    {
        "key": "scope",
        "value": "userclicks-tracking"
    }
]
```

### `avn service tags replace`

Replaces a tag associated with an Aiven service, deleting the any old
entry first.

<table>
  <thead>
    <tr><th>Parameter</th><th>Information</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>`service_name`</td>
      <td>The name of the service</td>
    </tr>
    <tr>
      <td>`--tag`</td>
      <td>The service tag to replace, in the format `KEY=VALUE`</td>
    </tr>
  </tbody>
</table>


**Example:** in the `demo-kafka` Aiven service, replace the tag with key
`scope` to the value `userclicks`

``` 
avn service tags replace demo-kafka \
    --tag scope=userclicks 
```

### `avn service tags update`

Update tags associated with an Aiven service.

<table>
  <thead>
    <tr><th>Parameter</th><th>Information</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>`service_name`</td>
      <td>The name of the service</td>
    </tr>
    <tr>
      <td>`--add-tag`</td>
      <td>The service tag to add, in the format `KEY=VALUE`</td>
    </tr>
    <tr>
      <td>`--remove-tag`</td>
      <td>The service tag key to remove</td>
    </tr>
  </tbody>
</table>


**Example:** in the `demo-kafka` Aiven service, modify the following:

-   add the tag with key `scope` and value `userclicks`
-   add the tag with key `bu` and value `emea`
-   remove the tag with key `team`

``` 
avn service tags update demo-kafka  \
    --add-tag scope=userclicks      \
    --add-tag bu=emea               \
    --remove-tag team=frontend
```