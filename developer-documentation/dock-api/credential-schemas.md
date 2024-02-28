# Credential Schemas

Schemas are useful when enforcing a specific structure on a collection of data like a Verifiable Credential. Data Verification schemas, for example, are used to verify that the structure and contents of a Verifiable Credential conform to a published schema. On the other hand, Data Encoding schemas are used to map the contents of a Verifiable Credential to an alternative representation format, such as a binary format used in a zero-knowledge proof.

## Endpoints

[POST /schemas](index.html.md#create-schema-responses)\
[GET /schemas](index.html.md#list-schemas-responses)\
[GET /schemas/{schemaId}](index.html.md#get-schema-parameters)\\

## Create Schema

Schemas are used to describe the structure of credentials, specifically the credential subject. It helps the issuer, holder, and verifier to unambiguously determine the claims contained within the credential. To create a schema, you need to define the object body using JSON schema.

### Parameters <a href="#create-schema-parameters" id="create-schema-parameters"></a>

<table><thead><tr><th width="109">Name</th><th width="82">In</th><th width="130">Type</th><th width="139">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>JSON-schema.</td></tr></tbody></table>

> POST /schemas REQUEST

```shell
curl --location --request POST https://api.dock.io/schemas \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
 "$schema": "http://json-schema.org/draft-07/schema#",
 "description": "Dock Schema Example",
 "type": "object",
 "properties": {
  "id": {
    "type": "string"
 },
 "emailAddress": {
  "type": "string",
  "format": "email"
 },
 "alumniOf": {
  "type": "string"
 }
 },
 "required": [
  "emailAddress",
  "alumniOf"
 ],
 "additionalProperties": false,
 "author": "{{did}}"
}'


```

```json-doc
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "description": "Dock Schema Example",
  "type": "object",
  "properties": {
    "id": {
      "type": "string"
    },
    "emailAddress": {
      "type": "string",
      "format": "email"
    },
    "alumniOf": {
      "type": "string"
    }
  },
  "required": [
    "emailAddress",
    "alumniOf"
  ],
  "additionalProperties": false,
  "author": "{{did}}"
}
```

### Responses <a href="#create-schema-responses" id="create-schema-responses"></a>

<table><thead><tr><th width="133">Status</th><th width="177">Meaning</th><th width="270">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will try to create schema.</td><td><a href="index.html.md#schemajobid">JobId</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid params, e.g., size not supported or not JSON.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

> 200 Response

```json
{
  "id": "1082",
  "data": {
    "schema": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "description": "Dock Schema Example 3",
      "type": "object",
      "properties": {
        "id": {
          "type": "string"
        },
        "emailAddress": {
          "type": "string",
          "format": "email"
        },
        "alumniOf": {
          "type": "string"
        }
      },
      "required": [
        "emailAddress",
        "alumniOf"
      ],
      "additionalProperties": false
    },
    "author": "did:dock:5FBZNTZ4eg2EBuvEcYdkEtAhCXhCEA8zmPzYTwexM3g13fkF",
    "signature": {
      "Secp256k1": "..."
    },
    "id": "https://schema.dock.io/TestSchema-V1-1695817897561.json",
    "uri": "https://schema.dock.io/TestSchema-V1-1695817897561.json"
  }
}
```

## List Schemas

Return a list of all schemas created by the authenticated user.

### Parameters <a href="#list-schemas-parameters" id="list-schemas-parameters"></a>

<table><thead><tr><th width="121">Name</th><th width="102">In</th><th width="109">Type</th><th width="124">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

> GET /schemas REQUEST

```shell
curl --location --request GET https://api.dock.io/schemas \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

### Responses <a href="#list-schemas-responses" id="list-schemas-responses"></a>

<table><thead><tr><th width="110">Status</th><th width="177">Meaning</th><th width="302">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return all schemas created by the user.</td><td>Inline</td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

> 200 Response

```json
[
  {
    "schema": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "description": "Dock Schema Example",
      "type": "object",
      "properties": {
        "id": {
          "type": "string"
        },
        "emailAddress": {
          "type": "string",
          "format": "email"
        },
        "alumniOf": {
          "type": "string"
        }
      },
      "required": [
        "emailAddress",
        "alumniOf"
      ],
      "additionalProperties": false
    },
    "author": "did:dock:5HcbppP8LjoJFYRV7PTLEyPy3ZUK9JCkzC4PQHuVF34gRhe6",
    "id": "https://schema.dock.io/TestSchema-V1-1695817897561.json",
    "uri": "https://schema.dock.io/TestSchema-V1-1695817897561.json"
  }
]
```

## Get Schema

Reading a Schema from the Dock chain can easily be achieved by using the `get` method which will return the JSON schema to a specific schema ID. The `schemaId`needs to be URL encoded (e.g. `/schemas/https%3A%2F%2Fschema.dock.io%2FTestSchema-V1-1695817897561.json`)

### Parameters <a href="#get-schema-parameters" id="get-schema-parameters"></a>

<table><thead><tr><th width="132">Name</th><th width="100">In</th><th width="111">Type</th><th width="113">Required</th><th>Description</th></tr></thead><tbody><tr><td>schemaId</td><td>path</td><td>String</td><td>true</td><td>A URL encoded schema id.</td></tr></tbody></table>

> GET /schemas/{schemaId} REQUEST

```shell
curl --location --request GET https://api.dock.io/schemas/{schemaId} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

### Responses <a href="#get-schema-responses" id="get-schema-responses"></a>

<table><thead><tr><th width="114">Status</th><th width="178">Meaning</th><th width="297">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and returns the requested Schema.</td><td>Inline</td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the schema was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

> 200 Response

```json
{
  "schema": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "description": "Dock Schema Example",
    "type": "object",
    "properties": {
      "id": {
        "type": "string"
      },
      "emailAddress": {
        "type": "string",
        "format": "email"
      },
      "alumniOf": {
        "type": "string"
      }
    },
    "required": [
      "emailAddress",
      "alumniOf"
    ],
    "additionalProperties": false
  },
  "author": "did:dock:5HcbppP8LjoJFYRV7PTLEyPy3ZUK9JCkzC4PQHuVF34gRhe6",
  "id": "https://schema.dock.io/TestSchema-V1-1695817897561.json",
  "uri": "https://schema.dock.io/TestSchema-V1-1695817897561.json"
}
```
