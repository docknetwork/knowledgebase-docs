# Credential Schemas

Schemas are useful when enforcing a specific structure on a collection of data like a Verifiable Credential. Data Verification schemas, for example, are used to verify that the structure and contents of a Verifiable Credential conform to a published schema. On the other hand, Data Encoding schemas are used to map the contents of a Verifiable Credential to an alternative representation format, such as a binary format used in a zero-knowledge proof.

Truvera credential schemas are using json schema format and should follow this structure [https://json-schema.org/understanding-json-schema/reference](https://json-schema.org/understanding-json-schema/reference)

## Create Schema

Schemas are used to describe the structure of credentials, specifically the credential subject. It helps the issuer, holder, and verifier to unambiguously determine the claims contained within the credential. To create a schema, you need to define the object body using JSON schema.

### Parameters <a href="#create-schema-parameters" id="create-schema-parameters"></a>

<table data-full-width="false"><thead><tr><th width="109">Name</th><th width="82">In</th><th width="130">Type</th><th width="139">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>JSON-schema.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/schemas" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## List Schemas

Return a list of all schemas created by the authenticated user.

### Parameters <a href="#list-schemas-parameters" id="list-schemas-parameters"></a>

<table data-full-width="false"><thead><tr><th width="121">Name</th><th width="102">In</th><th width="109">Type</th><th width="124">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/schemas" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## Get Schema

Reading a Schema from the blockchain can easily be achieved by using the `get` method which will return the JSON schema to a specific schema ID. The `schemaId`needs to be URL encoded (e.g. `/schemas/https%3A%2F%2Fschema.dock.io%2FTestSchema-V1-1695817897561.json`)

### Parameters <a href="#get-schema-parameters" id="get-schema-parameters"></a>

<table data-full-width="false"><thead><tr><th width="132">Name</th><th width="100">In</th><th width="111">Type</th><th width="113">Required</th><th>Description</th></tr></thead><tbody><tr><td>schemaId</td><td>path</td><td>String</td><td>true</td><td>A URL encoded schema id.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/schemas/{schemaId}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Delete Schema

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/schemas/{schemaId}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



