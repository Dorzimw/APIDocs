{{{
  "title": "Start Maintenance Mode",
  "date": "11-21-2014",
  "author": "Bryan Friedman",
  "attachments": []
}}}

Sends a the start maintenance mode operation to a list of servers and adds operation to queue. Calls to this operation must include a token acquired from the authentication endpoint. See the [Login API](../Authentication/login.md) for information on acquiring this token.

### When to Use It

Use this API operation when you want to explicitly start maintenance mode on multiple servers.

## URL

### Structure

    POST https://api.ctl.io/v2/operations/{accountAlias}/servers/startMaintenance

### Example

    POST https://api.ctl.io/v2/operations/ALIAS/servers/startMaintenance

## Request

### URI Parameters

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| AccountAlias | string | Short code for a particular account | Yes |

### Content Properties

| Name | Type | Description | Req. |
| --- | --- | --- | --- |
| serverIds | array | List of server IDs to start maintenance mode on. | Yes |

### Request Example

### JSON

    [
       "WA1ALIASWB01",
       "WA1ALIASWB02"
    ]

## Response

The response will be an array containing one entity for each server that the operation was performed on.

### Entity Definition

| Name | Type | Description |
| --- | --- | --- |
| server | string | ID of the server that the operation was performed on. |
| isQueued | boolean | Boolean indicating whether the operation was successfully added to the queue. |
| links | array | Collection of [entity links](../Getting Started/api-v20-links-framework.md) that point to resources related to this server operation. |
| errorMessage | string | If something goes wrong or the request is not queued, this is the message that contains the details about what happened. |

### Examples

#### JSON

    [
      {
        "server":"wa1aliaswb01",
        "isQueued":true,
        "links":[
          {
            "rel":"status",
            "href":"/v2/operations/alias/status/wa1-12345",
            "id":"wa1-12345"
          }
        ]
      },
      {
        "server":"wa1aliaswb02",
        "isQueued":false,
        "errorMessage":"The operation cannot be queued because the server cannot be found or it is not in a valid state."
      }
    ]